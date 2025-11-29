TYPE ConveyorStatus :
STRUCT
	Conveyor_ID: INT; // Conveyor number/ID
	Speed: REAL; // Percentage of speed
	Running: BOOL;
	State: ConveyorState;
	Ready : BOOL; //Interlock
END_STRUCT
END_TYPE
