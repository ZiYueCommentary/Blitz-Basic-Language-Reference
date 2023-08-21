# Functions

A function is defined using the `Function` keyword:

```basic
Function {funcname}{typetag}( {params} ) 
     {statements} 
End Function
```

* `{funcname}` is any valid identifier.
* `{typetag}` is the type of value returned by the function. If `{typetag}` is omitted, the function returns an integer value by default.
* `{params}` is a comma-separated list of variables which is passed to the function when it is called, each parameter may be given an optional type tag. Parameters are always local.

A function may use the `Return` statement to return a result. `Return` may optionally be followed by an expression.

If there is no `Return` statement, or a `Return` without any expression is used, the function returns a default value of `0` for numeric functions, an empty string (`""`) for string functions, or a `Null` object for custom-type functions.
