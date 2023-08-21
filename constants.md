# Constants

Constants may be of any basic data type. Constants are variables that have fixed values that will not change (ever) during the course of your program. These are useful tools for things like screen resolution variables, etc.

*   **Floating point constants** must include a decimal point.

    For example: `5` is an integer constant, but `5.0` is a floating point constant.
*   **String constants** must be surrounded by quotation marks.

    For example: `"This is a string constant"`.

The `Const` keyword is used to assign an identifier to a constant. For example:

```basic
Const one_hundred=100
```

You can then use the identifier `one_hundred` anywhere in your program instead of `100`.

A more useful example might be:

```basic
Const width=640,height=480
```

You can then use the more readable `width` and `height` throughout your program instead of `640` and `480`.

Also, if you ever decide to change the width and height values, you only have to do so at one place in the program.

There are two built-in **Integer constants** - `True` and `False`. `True` is equal to `1`, and `False` is equal to `0`.

There is also a built-in **floating-point constant** for _Pi_.
