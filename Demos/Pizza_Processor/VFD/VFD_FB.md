FUNCTION_BLOCK FB_VFD
VAR_INPUT
    bRunCmd           : BOOL;
    rSpeedSetpoint_Hz : REAL;
    bDirectionFwd     : BOOL := TRUE;
    bEStop            : BOOL;
    bLidClosed        : BOOL := TRUE;
    bUpstreamReady    : BOOL :=    TRUE;
    bDownstreamReady  : BOOL :=    TRUE;
END_VAR

VAR_OUTPUT
    Status       : VFDStatus;
    bRun         : BOOL;
    bForward     : BOOL;
    bReverse     : BOOL;
    rSpeedRef_Hz : REAL;
END_VAR

VAR
    trigRun    : R_TRIG;
    trigStop   : F_TRIG;

    // THIS ONE LINE REPLACES ALL YOUR MANUAL RAMP + CYCLE-TIME CODE
    rampVFD : Util.Ramp_Real := (
                    ASCEND   := 6.25,    // Hz per second ramp-up
                    DESCEND  := 8.00,    // Hz per second ramp-down (can be faster)
                    TIMEBASE := T#0s );  // ← AUTOMATIC cycle time (the correct way)

    tonAtSpeed : TON := (PT := T#800ms);
END_VAR
-------------------
// 1. Permissives
Status.Ready := bLidClosed AND bUpstreamReady AND bDownstreamReady AND NOT bEStop;

// 2. Triggers
trigRun (CLK := bRunCmd AND Status.Ready);
trigStop(CLK := bRunCmd);

// 3. Target frequency
Status.SpeedSetpoint_Hz := rSpeedSetpoint_Hz;  

// 4. OFFICIAL UTIL RAMP – only two lines forever
rampVFD( IN    := Status.SpeedSetpoint_Hz,  // REAL not BOOL
         RESET := NOT Status.Ready );


// 5. Use the perfect, cycle-independent ramped value
rSpeedRef_Hz := rampVFD.OUT;                       // this is your analog output
Status.Speed_Actual_Hz := rampVFD.OUT;

// 6. At-speed detection
tonAtSpeed(IN := ABS(Status.SpeedSetpoint_Hz - rampVFD.OUT) <= 2.0);
Status.IsAtSpeed := tonAtSpeed.Q;

// 7. State machine (exactly the same as before)
CASE Status.State OF
    VFDState.Stopped :
        IF trigRun.Q THEN
            Status.State := VFDState.Ramp_Up;
            Status.StartCount := Status.StartCount + 1;
        END_IF
    VFDState.Ramp_Up :
        IF Status.IsAtSpeed THEN Status.State := VFDState.Running; END_IF
    VFDState.Running :
        IF trigStop.Q OR Status.SpeedSetpoint_Hz <= 0.0 THEN
            Status.State := VFDState.Ramp_Down;
        END_IF
    VFDState.Ramp_Down :
        IF rampVFD.OUT <= 1.0 THEN Status.State := VFDState.Stopped; END_IF
    VFDState.E_Stop :
        IF Status.Ready THEN Status.State := VFDState.Stopped; END_IF
END_CASE;

IF NOT Status.Ready THEN Status.State := VFDState.E_Stop; END_IF;

// 8. Rest of outputs
Status.IsRunning  := (Status.State = VFDState.Ramp_Up) OR (Status.State = VFDState.Running);
Status.Direction   := bDirectionFwd;
Status.TimeStamp  := TIME();

bRun     := Status.IsRunning;
bForward := Status.IsRunning AND  Status.Direction;
bReverse := Status.IsRunning AND NOT Status.Direction;