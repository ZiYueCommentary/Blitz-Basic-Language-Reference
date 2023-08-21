# Program Flow

The following constructs are available for controlling program flow.

## If ... Then

```basic
If {expression} Then {statements1} Else {statements2} 
```

Evaluates the `If` expression and, if true, executes the `Then` statements. If false, the `Else` statement are executed, the `Else` part is optional - statements are executed until the end of the line.

```basic
If {expression1}
     {statements1} 
Else If {expression2}
     {statements2} 
Else If {expression3}
     {statements3}
Else 
     {statements4} 
EndIf
```

This form of the If statement allows for more than one line of statements. The `Else If` and `Else` parts are optional. The `Else` part is executed only if none of the `If` or `Else If` expressions were true.

## While ... Wend

```basic
While {expression} 
     {statements} 
Wend 
```

A While loop continues executing until `{expression}` evaluates to `False`. `{expression}` is evaluated at the start of each loop.

## For ... Next

```basic
For {variable}={initalvalue} To {finalvalue} Step {step} 
     {statements} 
Next 
```

A For/Next loop first assigns `{initialvalue}` to `{variable}` and then starts looping. The loop continues until `{variable}` reaches `{finalvalue}` and then terminates. In each loop, the value `{step}` is added to `{variable}`. If a step value is omitted, a default value of 1 is used.

This form of the For/Next loop allows you to iterate over all objects of a custom type.

## Repeat ... Until/Forever

```basic
Repeat 
     {statements} 
Until {expression} 
```

A Repeat loop continues executing until `{expression}` evaluates to `True`. `{expression}` is evaluated at the end of each loop.

```basic
Repeat 
     {statements} 
Forever
```

A Repeat/Forever loop simply executes `{statements}` until the program ends, or an `Exit` command is executed.

## Select ... Case

```basic
Select {expression} 
     Case {expressions1}
          {statements1} 
     Case {expressions2} 
          {statements2}
     Default 
          {statements3} 
End Select 
```

First the `Select` expression is evaluated. It is then compared with each of the `Case` expression lists. If it matches a `Case`, then the statements in the `Case` are executed.

If the `Select` expression matches none of the `Case` expressions, the statements in the optional `Default` section is executed.

## Breaking Out Of A Loop

The `Exit` command may be used to break out of any `For...Next`, `While...Wend`, `Repeat...Until` or `Repeat...Forever` loop.

## Using Includes

Blitz also supports the `Include` command. Include allows source code from an external file to be compiled as if it were part of the main program. Include must be followed by a quote enclosed filename. For example...

```basic
Include "anotherfile.bb"
```

Include allows you to break your program up into smaller, more manageable chunks.
