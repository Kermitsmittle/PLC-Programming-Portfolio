TYPE HopperStatus :
STRUCT
    Hopper_Id: INT;       //Hopper Location/ID
    State: HopperState;   //HopperState refering to ENUM
    Fill_Level: REAL;     //Hopper_Ingredient level
    Ingredient_ID: INT;   //Ingredient Name or Ingredient ID
    Alarm_Active: BOOL;   //Alarm Status
    Ready: BOOL ;         //Interlock
    StartCount: DINT;     //       
    LastFaultCode: INT;        
    Timestamp: TIME;       

END_STRUCT
END_TYPE
