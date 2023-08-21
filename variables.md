# Variables

Variables may be of any basic data type, or a custom type. A variable's type is determined by a special character that follows its identifier.

## Variable Types

These special characters are called **type tags** and are:

* `%` = Integer variables
* `#` = Floating point variables
* `$` = String variables
* `.{typename}` = Custom type variables

Here are some examples of valid variables:

* `Score%`
* `speed#`
* `name$`
* `player.Player`

The type tag only needs to be added the first time you use a variable, after that you can leave the type tag off if you wish.

If you don't supply a type tag the first time a variable is used, the variable defaults to an integer.

It is illegal to use the same variable name with a different type. For example, if you already have an integer variable called `name%`, it is illegal to also have a string variable called `name$`.

## Setting Variables

The `=` keyword is used to assign a value to a variable. For example: `score%=0` will assign the value `0` to the integer variable `score`.

## Variable Scope

Variables may also be either `Global`, or `Local`. This refers to where in a program a variable may be used.

* **Global variables** can be used from anywhere in the program.
* **Local variables** can only be used within the function they are created in.

The `Global` keyword is used to define one or more global variables. For example:&#x20;

```basic
Global Score=0,Lives=3,Player_up=1
```

Defines 3 global variables.

Similarly, `Local` is used to define local variables:&#x20;

```basic
Local temp_x=x,temp_y=y
```

If you use a variable without defining it as either local or global, it defaults to being local.
