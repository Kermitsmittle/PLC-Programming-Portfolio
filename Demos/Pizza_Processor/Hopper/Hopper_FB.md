FUNCTION_BLOCK FB_Hopper
VAR_INPUT
    StartDispense: BOOL;
    StopDispense: BOOL;
    ResetFault: BOOL;
    UpstreamReady: BOOL;
    DownstreamReady: BOOL;
    SimMode: BOOL;
END_VAR
VAR_OUTPUT
    Status: HopperStatus;
END_VAR

VAR
    Timer_LowLevel: TON; // timer for low level fault
END_VAR
// -----------------


// Main State Machine
CASE Status.State OF
	
    HopperState.OFF:
        IF UpstreamReady AND DownstreamReady THEN
            Status.State := HopperState.IDLE;
        END_IF

    HopperState.IDLE:
        Status.Ready := Status.Fill_Level > 10.0 AND NOT Status.Alarm_Active;
        IF StartDispense AND Status.Ready THEN
            Status.State := HopperState.DISPENSING;
            Status.StartCount := Status.StartCount + 1;
        END_IF
        IF Status.Fill_Level < 5.0 THEN
            Status.State := HopperState.LOW_LEVEL_FAULT;
        END_IF

    HopperState.DISPENSING:
        IF SimMode THEN
            Status.Fill_Level := Status.Fill_Level - 0.1; // simulate use
        END_IF
        IF StopDispense THEN
            Status.State := HopperState.IDLE;
        END_IF
        IF Status.Fill_Level < 5.0 THEN
            Status.State := HopperState.LOW_LEVEL_FAULT;
        END_IF

    HopperState.LOW_LEVEL_FAULT:
        Status.Alarm_Active := TRUE;
        Status.LastFaultCode := 101; // code for low level fault
        IF ResetFault AND Status.Fill_Level > 10.0 THEN
            Status.Alarm_Active := FALSE;
            Status.State := HopperState.IDLE;
        END_IF

    HopperState.BLOCKED:
        // implement other block conditions (e.g., jammed/fault inputs)
        IF ResetFault THEN
            Status.State := HopperState.IDLE;
        END_IF
    HopperState.MANUAL:    // In MANUAL, the operator can force DISPENSING or IDLE
        IF StartDispense THEN  
            Status.State := HopperState.DISPENSING;
        ELSIF StopDispense THEN
	          Status.State := HopperState.IDLE;
        END_IF

    // Interlock: even in manual, block if safety is lost
    IF NOT UpstreamReady OR NOT DownstreamReady THEN
        Status.State := HopperState.BLOCKED;
    END_IF

END_CASE

// Diagnostic update
Status.Timestamp := TIME(); // update time on every scan.