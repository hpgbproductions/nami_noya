# Label Value Substitution Format

This page discusses my findings on the curly brace format used to display results of Funky Trees in labels, based on a conversation among members of Funky Trees Lab. Undocumented label format specifiers were found in the labels on the main displays on the Wasp, and this article aims to explain the workings of this format.

Funky Trees value substitution terms can follow the form `{VALUE;FORMAT;UNITS}`, where:

- `VALUE` is the Funky Trees, same as the kind used in variables and Input Controllers,
- `FORMAT` is a format specifier, and
- `UNITS` converts the displayed value by a game-defined factor and appends the unit to the numeric value.

As the terms are used one after the other, using any term requires using all previous terms. It is only possible to specify a unit conversion if the format is specified.

## Label Format

The format specifier is defined in the System.NumberFormatter class, likely [this implementation](https://github.com/mono/mono/blob/main/mcs/class/corlib/System/NumberFormatter.cs) in Mono. Two styles of formats are allowed:

- [Standard numeric format strings](https://learn.microsoft.com/en-us/dotnet/standard/base-types/standard-numeric-format-strings)
- [Custom numeric format springs](https://learn.microsoft.com/en-us/dotnet/standard/base-types/custom-numeric-format-strings)

The following standard format specifiers **do not** work in SimplePlanes:

- Binary (B)
- Decimal (D)
- Hexadecimal (X)

However, the decimal format can be defined as a custom format by writing the desired number of zeroes. For example, the custom format `000` is equivalent to `D3`.

It is also possible to insert literal characters into custom numeric format strings. Rich text formatting defined inside the format string will work as normal. Such formatting can be used to create different styles for the value and its units.

## Label Units
