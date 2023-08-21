# Arrays

Arrays are created using the standard BASIC `Dim` statement, and may be of any number of dimensions. For example:&#x20;

```basic
Dim arr(10) 
```

Creates a one-dimensional array called `arr` with 11 elements numbered 0...10.

Arrays may be of any basic type or a custom type.

The type of an array is specified using a type tag. For example:&#x20;

```basic
Dim Deltas#(100)
```

Creates an array called `Deltas` of 101 floating point elements.

If the type tag is omitted, the array defaults to an integer array.

An array may be dimensioned at more than one point in a program, each time an array is dimensioned, it's previous contents are discarded. Arrays may be dimensioned inside functions, but a corresponding `Dim` statement of the same array must also appear somewhere in the main program. For example:

```basic
Dim test(0,0)
Function Setup( x,y )
    Dim test(x,y)
End Function
```
