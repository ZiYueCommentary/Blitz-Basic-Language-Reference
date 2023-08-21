# Custom Types

## What Are They?

**TYPE is your best friend.** It is used to create a "collection" of objects that share the same parameters and need to be interated through quickly and easily.

> Think about _SPACE INVADERS_. There are many aliens on the screen at one time. Each of these aliens have a few variables that they all need: x and y coordinates plus a variable to control which graphic to display (legs out or legs in).&#x20;
>
> Now, we could make hundreds of variables like `invader1x`, `invader1y`, `invader2x`, `invader2y`, etc. to control all the aliens, but that wouldn't make much sense would it? You could use an array to track them; invader(number,x,y,graphic), and the loop through them with a `FOR ... NEXT` loop but that is a lot of work!&#x20;
>
> The TYPE variable collection was created to handle just this sort of need.

`TYPE` defines an object collection. Each object in that collection inherits its own copy of the variables defined by the TYPE's `Field` command. Each variable of each object in the collection can be read individually and can be easily iterated through quickly. Use the `Field` command to assign the variables you want between the `Type` and `End Type` commands.

If it helps, think of a `TYPE` collection as a database. Each object is a record of the database, and every variable is a field of the record. Using commands like `Before`, `After`, and `For ... Each`, you can move to change the pointer of the "database" to point to a different record and retrieve/set the variable field values.

> Not a database guru? Need another example? Okay. Let's say you are setting up an auditorium for a speech or event and you are putting up hundreds of chairs for the spectators.&#x20;
>
> The chairs have to be in a certain place on the floor, and some will need to be raised up a bit higher than others (visiting dignitaries, the mayor is coming, etc.). So being the computer genius you are, you start figuring out how you can layout the chairs with the least amount of effort.&#x20;
>
> You realize that the floor is checkered, so its really a huge grid! This will make it easy! You just need to number the floor on a piece of graph paper and put into the grid how high each chair should be, based on where the boss told you the important people are to sit.&#x20;
>
> So, for each chair, you will have a row and column on the graph paper (x and y location) and a level to adjust the chair to (height). Good, we are organized. Now, even though we have it all on paper, we still have to do the work of placing all the chairs.&#x20;
>
> After you are done, let's say your boss walks up to you and says "they aren't centered right .. move'em all over 1 square". Ah crap! You have them all perfect, and even though it is a simple thing to move a chair one square to the right (after all, their order and height won't change) - you still have to move each and every chair!&#x20;
>
> Should would be nice if you could just wave your hand and say "For each chair in the room, add 1 square to its x location" and have it just magically happen. Alas, in the real world, get busy - you've got a lot of chairs to move!

In Blitz, you could have set up a TYPE called `CHAIR`, set the TYPE's FIELDS as `X`, `Y`, and `HEIGHT`. You would then create as many chairs as you need with the `New` command (each time you call `New`, it makes a new chair, with its OWN `X`, `Y`, and `HEIGHT` variables) and assign them the `X`, `Y`, and `HEIGHT` values you decide upon.

In our example above, when the boss told you to move the chairs over 1 box, you probably groaned inside. That's a lot of work! In Blitz, we could use four lines of code to adjust all our `CHAIR` objects to the new position (using `For ... Each` commands).

## Defining A Type

Custom types are defined using the `Type` keyword. For example:

```basic
Type MyType 
    Field x, y 
End Type
```

Creates a custom type called `MyType` with 2 fields - `x` and `y`.

Fields within a custom type may themselves be of any basic type or custom type. Type tags are used to determine the type of a field. For example:

```basic
Type MyType 
    Field x, y 
    Field description$ 
    Field delta_x#, delta_y# 
End Type 
```

## Creating a Type Instance

You can create variables or arrays of custom types using a "`.`" type tag followed by the type name. For example:

```basic
Global mine.MyType 
Dim all_mine.MyType( 100 ) 
```

Before a custom type variable or array element can be used, it must be initialized using the New operator. For example:

```basic
mine.MyType = New MyType
```

The `New` operator creates an "object" of type `MyType`, and returns a "pointer" to the new object. The identifier following the `New` operator must be a valid custom type name.

The fields within a custom type are accessed using the "`\`" character. For example:&#x20;

```basic
mine\x=100
Print mine\x
```

## Destroying a Type Instance

When you've finished with an object, you should delete it using the `Delete` command. For example:

```basic
Delete mine
```

This releases the memory used by the object.

## Determining Existance

The special keyword `Null` is used to represent non-existent objects. An object is non-existent if it hasn't been initialized yet using `New`, or has been released using `Delete`. For example:

```basic
mine.MyType=New MyType 
If mine<>Null 
     Print "exists!" 
Else 
     Print "doesn't exist!" 
EndIf 
Delete mine 
If mine<>Null 
     Print "exists!" 
Else 
     Print "doesn't exist!" 
EndIf 
```

...will print the following:

```
exists! 
doesn't exist!
```

Each custom type has an associated list of objects known as a "**type list**". When an object is created using `New`, it is automatically added to the type list. When an object is released using `Delete`, it is removed from the type list. This list is dynamic - once an instance has been deleted, its place in the collection is deleted and all the other objects after it will "move up" in the collection hiearchy.

## Iteration Through Type Lists

The `First`, `Last`, `After` and `Before` operators allow you to access type lists. The `First` operator returns the object at the start of the type list. For example:

```basic
mine.MyType = First MyType
```

This sets the `mine.MyType` variable to the first object of custom type `MyType`.

Similarly, `Last` returns the object at the end of the list.

If the type list is empty, `First` and `Last` return `Null`.

You can use `After` to find the object after an object, and `Before` to find the object before an object. For example:

```basic
mine.MyType = First MyType ;mine=first object in the type list 
mine = After(mine) ;mine=second object 
mine = After(mine) ;mine=third object 
mine = Before(mine) ;mine=second object 
mine = Before(mine) ;mine=first again! 
```

`After` and `Before` return `Null` if there is no such object. For example:

```basic
mine.MyType = Last MyType ;mine=last object 
mine = After(mine) ;object after last does not exist! 
```

When an object is created using `New`, it is placed at the end of it's type list by default. However, You can move objects around within the type list using Insert. For example:

```basic
mine1.MyType = New MyType
mine2.MyType = New MyType 
Insert mine2 Before mine1
```

This has the effect of placing the "mine2" object before the "mine1" object in the type list. You can also use `After` instead of `Before` with `Insert`.

Here's an example of moving an object to the start of it's type list:

```
Insert mine Before First MyType
```

A special form of `For...Next` allows you to easily iterate over all object of a custom type. For example:

```basic
For mine.MyType = Each MyType 
    ...
Next
```

This will cause the variable `mine.MyType` to loop through all existing objects of cutom type `MyType`.

Finally, the `Delete Each` command allows you to delete all objects of a particular type. For example:

```basic
Delete Each MyType
```
