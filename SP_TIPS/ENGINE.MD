### FT Engine (first generation)

For the simulation of vehicles with internal combustion engines. Current applications:

- ALPACA (KT10-A)

Notice:

- Setters of VR input handler variables must have a priority of -1 or lower, even if they are placed before the engine setters.

| Priority | Name | Structure | Comments |
| --- | :--- | :--- | :--- |
| -100 | DeltaTime | `Time-PreviousTime` | Time between this update and the previous update. |
| 0 | TimeSinceGearChange | TIMER WITH RESET FUNCTION | Timer is reset when a gear shift is commanded. |
| 0 | GearSelected | (unspecified) | Zero is neutral, positive numbers are forward gears, and negative numbers are reverse gears. Other gear number assignments can also be chosen. It is possible to add debounce using TimeSinceGearChange. |
| 0 | GearRatio | TERNARY VALUE LIST | List of gear ratios. Reverse gear ratios are negative. Neutral gear ratio is defined as zero as gear ratio multiplies with engine input. Include a multiplier for final drive. |
| 0 | WheelRpm | AVERAGE OF VALUES | Average RPM of all driven wheels. Remember that wheel RPM sign is different on each side of the car. DO NOT use RPM readouts from engines as they are unsigned. |
| 0 | EngineRpm | `clamp(WheelRpm * GearRatio, MIN, MAX)` | RPM when not in neutral. Used for engine input calculations. |
| 0 | TargetRpmInNeutral | `lerp(MIN, MAX, PLAYERINPUT_THROTTLE)` | Neutral RPM controller can be improved. |
| 0 | EngineRpm | FIXED INTERVAL PROPORTIONAL CONTROLLER | RPM when in neutral. For sound effects only. Activator is used to check that the vehicle is in neutral gear. |
| 0 | MaxEngineInput | LINEAR MAP CHAIN | Value when engine throttle is full. Torque curve. |
| 0 | MinEngineInput | LINEAR MAP CHAIN | Value when engine throttle is zero. Engine braking curve.
| 0 | FrontEngineInput | MULTIPLY( `GearRatio`, ENGINE INPUT, OTHER EFFECTS) | To front axle engine. Effects include smoothing and torque distribution. |
| 0 | RearEngineInput | MULTIPLY( `GearRatio`, ENGINE INPUT, OTHER EFFECTS) | To rear axle engine. |
| 100 | PreviousTime | `Time` | Store the update time for the calculation of DeltaTime in the next update. |
