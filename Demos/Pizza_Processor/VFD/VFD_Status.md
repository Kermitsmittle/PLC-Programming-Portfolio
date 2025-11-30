TYPE VFDStatus :
STRUCT
	//Identification
    VFD_ID : STRING[20];
    State : VFDState;
	Direction : BOOL; //True = Forward , False = Reverse
	
	//Speed
	SpeedSetpoint_Hz  : REAL; 
    Speed_Actual_Hz   : REAL;   
	
	//Status
	IsRunning : BOOL;
	IsAtSpeed : BOOL;
	Ready : BOOL;
	
	//Alarms
	Alarm_Active : BOOL;
	LastFault_Code : INT ;
	Interlock_Reason : STRING [50];
	
	//Counters
	StartCount : UDINT;
	RunTime_Hours : REAL;
	
	//Hardware_DATA
	Current : REAL;
	Torque_Percentage : REAL;
	
	//Comms
	Comm_OK : BOOL ;
	Comms_Fault_Code : INT;
	
	//TimeStamp
	TimeStamp : TIME;
	

END_STRUCT
END_TYPE

