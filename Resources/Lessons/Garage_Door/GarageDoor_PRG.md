PROGRAM GarageDoor_PRG
VAR
	    Motor1 : FB_Motor;  // Instance of your motor FB

    // Inputs simulation (replace with actual I/O in real hardware)
    bOpenCmd : BOOL := FALSE;
    bCloseCmd : BOOL := FALSE;
    bEStop   : BOOL := FALSE;
    bReset   : BOOL := FALSE;

    // Sensors simulation
    bUpLimitSensor   : BOOL := FALSE;
    bDownLimitSensor : BOOL := FALSE;
END_VAR
---------------

// Update motor inputs
Motor1.Open := bOpenCmd;
Motor1.Close := bCloseCmd;
Motor1.E_Stop := bEStop;
Motor1.ResetFault := bReset;

// Simulate sensor inputs inside Status struct (assuming you can set these from outside)
Motor1.Status.UpLimit := bUpLimitSensor;
Motor1.Status.DownLimit := bDownLimitSensor;

// Run the motor FB logic
Motor1();
