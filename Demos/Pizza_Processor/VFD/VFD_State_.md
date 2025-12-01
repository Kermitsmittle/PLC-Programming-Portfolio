'''

 TYPE VFDState :(
     Ramp_up, // Ramp-up Phase
     Running,// Normal operation
     Ramp_Down,// Controlled deceleration
     Stopped,// VFD Stopped
     Idle, //VFD Powered but not running
     Fault,// VFD in Fault State
     E_Stop // E-Stop Condition
    );
END_TYPE

'''
