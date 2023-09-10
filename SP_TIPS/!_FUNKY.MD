# Funky Forest

A list of Funky Trees that I find useful. Notes:

- Replace variable names in ALL CAPS to your own values or variables.
- List of variables may not be in the same order as the Funky Trees. The list order is chosen for readability.
- Expected data types are provided. Some codes require preceding variable setters.

## Common

Funky Trees with general applications.

### Animation / Delay Timer

`smooth(ACTIVE ? 0 : PERIOD, 1)`

General purpose smooth-based timer for animations. When `ACTIVE` is TRUE, counts towards `PERIOD`. Otherwise, counts towards zero. This shows the key principles of timers based on the smooth function. This timer can be used as the field of `VAL` in the Linear Value Map.

- `bool ACTIVE`: Boolean input value.
- `float PERIOD`: Total duration of the animation.

### Linear Value Map (Clamped)

`lerp(TO_LOW, TO_HIGH, inverselerp(FROM_LOW, FROM_HIGH, VAL))`

Maps a value `VAL` in the range `FROM_LOW..FROM_HIGH` to the range `TO_LOW..TO_HIGH`. The output is clamped between `TO_LOW` and `TO_HIGH`. This is equivalent to the Arduino code `constrain(map(VAL, FROM_LOW, FROM_HIGH, TO_LOW, TO_HIGH), TO_LOW, TO_HIGH)`.

- `float VAL`: Input value.
- `float FROM_LOW`: Input range, lower bounds.
- `float FROM_HIGH`: Input range, upper bounds.
- `float TO_LOW`: Output range, lower bounds. Minimum output value.
- `float TO_HIGH`: Output range, upper bounds. Maximum output value.

### Linear Value Map (Unclamped)

`TO_LOW + (VALUE - FROM_LOW) / (FROM_HIGH - FROM_LOW) * (TO_HIGH - TO_LOW)`

Maps a value `VALUE` in the range `FROM_LOW..FROM_HIGH` to the range `TO_LOW..TO_HIGH`. The output is unclamped. This is equivalent to the Arduino code `map(VALUE, FROM_LOW, FROM_HIGH, TO_LOW, TO_HIGH)`.

- `float VALUE`: Input value.
- `float FROM_LOW`: Input range, lower bounds.
- `float FROM_HIGH`: Input range, upper bounds.
- `float TO_LOW`: Output range, lower bounds.
- `float TO_HIGH`: Output range, upper bounds.

### One-Way Activation Delay

`sum(sum(ACTIVE?1:0)>0 ? 1 : 0) > DELAY`

A very basic solution to activate a part `DELAY` seconds after `ACTIVE` is TRUE. The inner `sum` function and comparison prevent the cancellation of the action.

- `bool ACTIVE`: Boolean input value.
- `float DELAY`: Delay in seconds.

### Smooth with Different Attack/Decay

`smooth(VALUE, SELF<VALUE ? ATTACK : DECAY)`

**[ SETTER ONLY ]** This can only be used as a variable setter. It cannot be used directly in an Input Controller.

The smoothed value increases and decreases at different rates, known as attack and decay rates respectively.

- `float VALUE`: Input value to be smoothed out.
- `float SELF`: Same as the variable setter name.
- `float ATTACK`: Maximum rate of increase.
- `float DECAY`: Maximum rate of decrease.

### Sum Replacement with Clamp

`smooth(sum(1)<0.1 ? START_VALUE : (INPUT<0 ? MIN_VALUE : MAX_VALUE), abs(INPUT))`

A simple alternative to the sum function which allows the addition of clamping limits. There is no perceived delay near clamping limits.

- `float START_VALUE`: Value to initialize the function with, usually 0.
- `float MIN_VALUE`: Minimum output value.
- `float MAX_VALUE`: Maximum output value.
- `float INPUT`: Input that corresponds to the argument of `sum(...)`.

### Sum Replacement / Timer with Reset

`smooth(!RESET & sum(1)>0.1 ? MAX_VALUE : RESET_VALUE, !RESET & sum(1)>0.1 ? SPEED : CONST_POSITIVE_LARGE)`

When `RESET` is FALSE, counts towards MAX_VALUE the rate of `SPEED`. When `RESET` is TRUE, moves the value quickly towards `RESET_VALUE`.

The `sum(1)>0.1` component forces the ternary statement to start FALSE, so the starting value is always `RESET_VALUE`.

- `bool RESET`: Input to reset the output.
- `float RESET_VALUE`: The function will return to this value when reset.
- `float MAX_VALUE`: Maximum output value.
- `float SPEED`: The rate of counting, same as the argument in `sum(x)`. Use 1 for timers.
- `float CONST_POSITIVE_LARGE`: Large number (try 999999).

## Controls

### Flight Stick Direction

`atan2(Roll, Pitch)`

Corresponds to a target angle of slip on VTOL applications.

## Combat System

### Target GS

`sqrt(pow(rate(RELATIVE_TARGET_X),2) + pow(rate(RELATIVE_TARGET_Y),2) + pow(rate(RELATIVE_TARGET_Z),2))`

- `Setter RELATIVE_TARGET_X`: `TargetDistance * sin(TargetHeading)`
- `Setter RELATIVE_TARGET_Y`: `TargetDistance * sin(TargetElevation)`
- `Setter RELATIVE_TARGET_Z`: `TargetDistance * cos(TargetHeading)`

### Target World Coordinates

- `Longitude + TargetDistance * sin(TargetHeading)`
- `Altitude + TargetDistance * sin(TargetElevation)`
- `Latitude + TargetDistance * cos(TargetHeading)`

## Scientific

Funky Trees based on common scientific equations.

### Centripetal Acceleration (m/s<sup>2</sup>)

`LOCAL_ROTATION_RATE * GS * pi / 180`

Determines the G-force from rotation on the main cockpit block around the selected axis of rotation. The G-force components from gravity and acceleration are NOT considered. Use a further division of 9.81 to convert from m/s<sup>2</sup> to Gs.

- `float LOCAL_ROTATION_RATE`: Use `PitchRate`, `YawRate`, or `RollRate`.

### Kinetic Power (W)

`0.5 * MASS_KG * GS * GS`

Gets the rate of change of kinetic energy. Remove drag on your aircraft first if you want to find your engine power.

- `float MASS_KG`
