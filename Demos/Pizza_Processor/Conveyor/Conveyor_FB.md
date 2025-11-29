FUNCTION_BLOCK FB_Conveyor
VAR_INPUT
	Start: BOOL;
    Stop: BOOL;
    ResetFault: BOOL;
    UpstreamReady: BOOL;
    DownstreamReady: BOOL;
    SimMode: BOOL;
	Speed_Setpoint: REAL; //percentage in speed
	
END_VAR
VAR_OUTPUT
	Current_Speed: REAL; //
	Status: ConveyorStatus; 
END_VAR

VAR
	
END_VAR


---------

IF NOT UpstreamReady OR NOT DownstreamReady THEN
    Status.State := ConveyorState.JAM_FAULT;
ELSE
    CASE Status.State OF
        ConveyorState.OFF:
            Status.Running := FALSE;
            Current_Speed := 0.0;
            Status.Ready := FALSE;
            IF UpstreamReady AND DownstreamReady THEN
                Status.State := ConveyorState.IDLE;
            END_IF

        ConveyorState.IDLE:
            Status.Running := FALSE;
            Current_Speed := 0.0;
            Status.Ready := TRUE;
            IF Start THEN
                Status.State := ConveyorState.ON;
            END_IF

        ConveyorState.ON:
            Status.Running := TRUE;
            Current_Speed := Speed_Setpoint;
            Status.Speed := Speed_Setpoint;
            Status.Ready := TRUE;
            IF Stop THEN
                Status.State := ConveyorState.OFF;
            END_IF

        ConveyorState.JAM_FAULT:
            Status.Running := FALSE;
            Current_Speed := 0.0;
            Status.Ready := FALSE;
            IF ResetFault THEN
                Status.State := ConveyorState.IDLE;
            END_IF

        ConveyorState.MANUAL:
            IF Start THEN
                Status.State := ConveyorState.ON;
            ELSIF Stop THEN
                Status.State := ConveyorState.OFF;
            END_IF
    END_CASE
END_IF
