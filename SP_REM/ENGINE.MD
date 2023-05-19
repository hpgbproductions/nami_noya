### FT Engine (first generation)

For the simulation of vehicles with internal combustion engines. Current applications:

- ALPACA (KT10-A)

Notice:

- Setters of VR input handler variables must have a priority of -1 or lower, even if they are placed before the engine setters.

| Priority | Name | Structure | Comments |
| --- | :--- | :--- | :--- |
| -100 | DeltaTime | `Time-PreviousTime` | Time between this update and the previous update. |
| 0 | TimeSinceGearChange | RESET/RUN TIMER | |
| 0 | GearSelected | (unspecified) | It is possible to add debounce using TimeSinceGearChange. |
| 0 | GearRatio | TERNARY TREE | |
| 0 | WheelRpm | (unspecified) | Average RPM of all driven wheels. DO NOT use RPM from engines. |
| 0 | EngineRpm | `clamp(WheelRpm * GearRatio, MIN, MAX)` | RPM when not in neutral. Used for engine input calculations. |
| 0 | TargetRpmInNeutral | `lerp(MIN, MAX, PLAYERINPUT_THROTTLE)` | |
| 0 | EngineRpm | FIXED INTERVAL PROPORTIONAL CONTROLLER | RPM when in neutral. For sound effects only. |
| 0 | MaxEngineInput | LINEAR MAP CHAIN | Value when engine throttle is full. Torque curve. |
| 0 | MinEngineInput | LINEAR MAP CHAIN | Value when engine throttle is zero. Engine braking curve.
| 0 | FrontEngineInput | (unspecified) | To front axle engine. |
| 0 | RearEngineInput | (unspecified) | To rear axle engine. |
