# Funky Forest

A list of Funky Trees that I find useful and often use. Notes:

- Replace variable names in ALL CAPS to your own values or variables.
- List of variables may not be in the same order as the Funky Trees. The list order is chosen for readability.

## Common

Funky Trees with general applications.

### Linear Value Map (Clamped)

`lerp(TO_LOW, TO_HIGH, inverselerp(FROM_LOW, FROM_HIGH, VAL))`

Maps a value `VAL` in the range `FROM_LOW..FROM_HIGH` to the range `TO_LOW..TO_HIGH`. The output is clamped between `TO_LOW` and `TO_HIGH`. This is equivalent to the Arduino code `constrain(map(VAL, FROM_LOW, FROM_HIGH, TO_LOW, TO_HIGH), TO_LOW, TO_HIGH)`.

- `float VAL`: Input value.
- `float FROM_LOW`: Input range, lower bounds.
- `float FROM_HIGH`: Input range, upper bounds.
- `float TO_LOW`: Output range, lower bounds. Minimum output value.
- `float TO_HIGH`: Output range, upper bounds. Maximum output value.

### Linear Value Map (Unclamped)

`TO_LOW + (VAL - FROM_LOW) / (FROM_HIGH - FROM_LOW) * (TO_HIGH - TO_LOW)`

Maps a value `VAL` in the range `FROM_LOW..FROM_HIGH` to the range `TO_LOW..TO_HIGH`. The output is unclamped. This is equivalent to the Arduino code `map(VAL, FROM_LOW, FROM_HIGH, TO_LOW, TO_HIGH)`.

- `float VAL`: Input value.
- `float FROM_LOW`: Input range, lower bounds.
- `float FROM_HIGH`: Input range, upper bounds.
- `float TO_LOW`: Output range, lower bounds.
- `float TO_HIGH`: Output range, upper bounds.

### Sum() Replacement / Timer with Reset

`smooth(!RESET & sum(1)>0.1 ? MAX_VALUE : RESET_VALUE, !RESET ? SPEED : CONST_POSITIVE_LARGE)`

When `RESET` is FALSE, counts at the rate of `SPEED`. When `RESET` is TRUE, moves the value quickly towards `RESET_VALUE`.

- `bool RESET`: Input to reset the output.
- `float RESET_VALUE`: The function will return to this value when reset.
- `float MAX_VALUE`: Maximum output value.
- `float SPEED`: The rate of counting, same as the argument in `sum(x)`. Use 1 for timers.
- `float CONST_POSITIVE_LARGE`: Large number (try 999999).

## Flight Controls

## Scientific
