# Funky Forest

A list of Funky Trees that I find useful and often use. Replace variable names in ALL CAPS to your own values or variables.

## Common

Funky Trees with general applications.

### Linear Value Mapping (Clamped)

`lerp(TO_LOW, TO_HIGH, inverselerp(FROM_LOW, FROM_HIGH, VAL))`

Maps a value `VAL` in the range `FROM_LOW..FROM_HIGH` to the range `TO_LOW..TO_HIGH`. The output is clamped between `TO_LOW` and `TO_HIGH`. This is equivalent to the Arduino code `constrain(map(VAL, FROM_LOW, FROM_HIGH, TO_LOW, TO_HIGH), TO_LOW, TO_HIGH)`.

- `float TO_LOW`: Output range, lower bounds
- `float TO_HIGH`: Output range, upper bounds
- `float FROM_LOW`: Input range, lower bounds
- `float FROM_HIGH`: Input range, upper bounds
- `float VAL`: Input value

## Flight Controls

## Scientific
