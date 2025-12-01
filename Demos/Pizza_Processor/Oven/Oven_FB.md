FUNCTION_BLOCK Oven_FB
VAR_INPUT
    start_cmd : BOOL;      (* Rising edge to start *)
    stop_cmd : BOOL;       (* Rising edge to stop *)
    timer_set : TIME;      (* Set time e.g. T#10s *)
END_VAR
VAR_OUTPUT
    coil_on : BOOL;
    fan_on : BOOL;
    state : Oven_State;
    process_done : BOOL;
END_VAR
VAR
    start_time : TIME;
    elapsed_time : TIME;
    running : BOOL;
    start_edge : R_TRIG;
    stop_edge : R_TRIG;
END_VAR
-----------------------------------------------------------------
FUNCTION_BLOCK Oven_FB
VAR_INPUT
    start_cmd : BOOL;      (* Rising edge to start *)
    stop_cmd : BOOL;       (* Rising edge to stop *)
    timer_set : TIME;      (* Set time e.g. T#10s *)
END_VAR
VAR_OUTPUT
    coil_on : BOOL;
    fan_on : BOOL;
    state : Oven_State;
    process_done : BOOL;
END_VAR
VAR
    start_time : TIME;
    elapsed_time : TIME;
    running : BOOL;
    start_edge : R_TRIG;
    stop_edge : R_TRIG;
END_VAR
