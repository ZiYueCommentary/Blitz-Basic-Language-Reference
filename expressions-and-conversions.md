# Expressions and Conversions

The following operators are supported, listed in order of precedence:

| Keywords                        | Category                                         | Type   |
| ------------------------------- | ------------------------------------------------ | ------ |
| `New`, `First`, `Last`          | Custom type operators                            | Unary  |
| `Before`, `After`               | Object operators                                 | Unary  |
| `Int`, `Float`, `Str`           | Type conversion operators                        | Unary  |
| `+`, `-`, `~`                   | Arithmetic posate(?), Negate, Bitwise complement | Unary  |
| `^`                             | Arithmetic "to-the-power-of"                     | Binary |
| `*`, `/`, `Mod`                 | Arithmetic multiply, divide, remainder           | Binary |
| `Shl`, `Shr`, `Sar`             | Bitwise shift operators                          | Binary |
| `+`, `-`                        | Arithmetic add, Subtract                         | Binary |
| `<`, `>`, `<=`, `>=`, `=`, `<>` | Comparison operators                             | Binary |
| `And`, `Or`, `Xor`              | Bitwise And, Or and Exclusive Or                 | Binary |
| `Not`                           | Logical Not                                      | Unary  |

**Unary operators** take one operand, while **Binary operators** take two.

Arithmetic operators produce a result of the same type as the operands. For example, adding two integers produces an integer result.

If the operands of a binary arithmetic or comparison operator are not of the same type, one of the operands is converted using the following rules:

*   If one operand is a custom-type object, the other must be an object of the same type, or Null.

    Else if one operand is a string, the other is converted to a string.

    Else if one operand is floating point, the other is converted to floating point.

    Else both operands must be integers.

When floating point values are converted to integer, the value is rounded to the nearest integer. When integers and floating point values are converted to strings, an ascii representation of the value is produced.

When strings are converted to integer or floating point values, the string is assumed to contain an ascii representation of a numeric value and converted accordingly. Conversion stops at the first non-numeric character in the string, or at the end of the string.

The only arithmetic operation allowed on string is `+`, which simply concatenates the two operands.

Int, Float, and Str can be used to convert values. They may be optionally followed by the appropriate type tag - ie: `Int%`, `Str$` and `Float#`.

Comparison operators always produce an integer result: 1 for true, 0 for false.

If one of the operators is a custom-type object, the other must be an object of the same type, or `Null`, and the only comparisons allowed are `=>` and `<>`.

Bitwise and logical operators always convert their operands to integers and produce an integer result.

The `Not` operator returns 0 for a non-zero operand, otherwise 1. When an expression is used to conditionally execute code - for example, in an `If` statement - the result is converted to an integer value. A non-zero result means true, a zero result means false.
