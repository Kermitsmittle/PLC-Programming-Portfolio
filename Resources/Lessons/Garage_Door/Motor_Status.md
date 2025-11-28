TYPE Motor_Status : 
STRUCT
    Direction    : BOOL;      // TRUE = Forward, FALSE = Reverse
    State        : Motor_State;
    UpLimit      : BOOL;      // Sensor: door fully open
    DownLimit    : BOOL;      // Sensor: door fully closed
    E_Stop       : BOOL;      // Emergency stop input
    bRun         : BOOL;      // Motor run command
    Alarms       : BOOL;      // Alarm flag
    Fault_Code   : INT;       // 1=NoFault, 2=Jam, 3=NoPower, 99=EStop
    Ready        : BOOL;      // Interlock status
    Motor_Power  : BOOL;      // Motor power output
    Jam          : BOOL;      // Jam detection indicator
END_STRUCT
END_TYPE
