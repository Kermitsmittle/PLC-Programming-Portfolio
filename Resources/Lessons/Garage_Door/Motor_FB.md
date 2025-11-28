FUNCTION_BLOCK FB_Motor
VAR_INPUT
	Open       : BOOL;
	Close      : BOOL;
	E_Stop     : BOOL;
	ResetFault : BOOL;

END_VAR
VAR_OUTPUT
	Status : Motor_Status;
END_VAR
VAR
	InProcess : BOOL;
	TimerOpen : TON;
	TimerClose: TOF;
END_VAR
------------------------------------------
/// Fault reset logic

IF ResetFault AND Status.State = Fault THEN
    Status.State := Closed;     // Change as per your system start-up state
    Status.Alarms := FALSE;
    Status.Fault_Code := 1;     // No fault
    Status.E_Stop := FALSE;
    Status.Motor_Power := FALSE;
END_IF

// Immediate E-Stop handling: override everything
IF E_Stop THEN
    Status.State := Fault;
    Status.Alarms := TRUE;
    Status.Fault_Code := 99;    // E-Stop fault code
    Status.Motor_Power := FALSE;
    RETURN;                    // Immediately stop processing
END_IF

// State machine controlling the motor
CASE Status.State OF

    Opening:
        Status.Direction := TRUE;           // Forward
        Status.Motor_Power := TRUE;
        TimerOpen(IN := Open);

        // Transition when fully open or timer done
        IF Status.UpLimit OR TimerOpen.Q THEN
            Status.State := Opened;
            Status.Motor_Power := FALSE;
            TimerOpen(IN := FALSE);        // Reset timer
        END_IF;

        // Handle jam or other faults here (expand as needed)

    Opened:
        Status.Motor_Power := FALSE;
        IF Close THEN
            Status.State := Closing;
        END_IF;

    Closing:
        Status.Direction := FALSE;          // Reverse
        Status.Motor_Power := TRUE;
        TimerClose(IN := Close);

        // Transition when fully closed or timer done
        IF Status.DownLimit OR TimerClose.Q THEN
            Status.State := Closed;
            Status.Motor_Power := FALSE;
            TimerClose(IN := FALSE);        // Reset timer
        END_IF;

    Closed:
        Status.Motor_Power := FALSE;
        IF Open THEN
            Status.State := Opening;
        END_IF;

    Fault:
        Status.Motor_Power := FALSE;
        // Remains in fault until reset
        // Could add blinking alarm, logging here

END_CASE;
