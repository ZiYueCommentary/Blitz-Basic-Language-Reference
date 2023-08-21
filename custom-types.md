# 自定类型

## 什么是自定类型？

**自定类型是你最好的朋友。**它被用于创建拥有相同参数的对象的“集合”，并且快速轻松地进行交互。

> 想象一下《太空入侵者》，现在屏幕上有很多的外星人。每一个外星人都有一些需要的变量：x、y 和一个控制画面显示的变量（腿向外或向内）。
>
> 现在，我们可以创建数百个变量，例如 `invader1x`、`invader1y`、`invader2x`、`invader2y` 来控制所有的外星人。但是这没多大意义，不是吗？你可以用数组来储存它们，并且使用 `For ... Next` 循环，但是这太麻烦了！
>
> “自定类型变量集合”就是用来解决这种问题的。

`Type` 能够定义一个对象集合。每个对象都会获得类型中 `Field` 定义的变量的副本。集合中每个对象的每个变量都可以单独读取，并且可以快速迭代。使用 `Field` 命令在 `Type` 和 `End Type` 中间定义所需的变量。

如果有帮助的话，您可以将类型集合想象成一个数据库。每个对象都是数据库的记录，每个变量都是记录中的字段。使用 `Before`、`After` 和 `For ... Each` 命令，您可以移动“数据库”的指针来指向不同的记录，以检索并设置变量的字段值。

> 不是数据库专家？还需要举个例子？没问题。想象你正在为一场演讲或一次活动搭建场景，你将要为观众摆数百把椅子。
>
> 椅子必须要放在地板上的某个地方，而有些椅子会比其他椅子高一点（比如老板和市长的椅子）。所以，作为电脑天才，你正在想办法最快最好地来布置椅子。
>
> 你意识到地板是方格的，地板完全是一个巨大的网格！弄这事更简单了！你只需要在一张图纸上对地板进行编号，并根据老板告诉你的重要人物的座位，将每张椅子的高度写到网格表上。
>
> 所以，每把椅子有会有一个 x 和 y，并会有一个水平高度来表示椅子的高度（height）。很好，我们逻辑很清晰。现在，尽管我们把这些东西都写在图纸上了，我们仍旧需要自己去放椅子。
>
> 当你完成之后，你的老板走到你面前说：“它们没有居中，把它们向右平移一米。”我操！本来这些东西都很完美。尽管椅子右移一米这事不难（毕竟它们的高度和顺序不会改变），但是你仍旧要一把一把挪这些椅子！
>
> 如果你能挥挥手说：“房间里的椅子的 x 都增加一个方格”，然后它们奇迹的挪过去了，那就太棒了。但是现实是——这些椅子都要你自己搬！

在 Blitz 中，你可以设置一个叫做 `Chair` 的类型，然后将类型的字段（Field）设置为 `x`、`y` 和 `height`。您可以使用 `New` 命令来创建所需数量的椅子（每次调用 `New` 时，它都会生成一把带有属于自己的 `x`、`y` 和 `height` 的新的椅子），并为他们分配由您决定的 `x`、`y` 和 `height`。

在上面的例子中，当老板让你把椅子挪动一格的时候，你可能会叫苦连天——这活可不少！但是在 Blitz 中，我们可以用四行代码让所有的 `Chair` 对象调整到新位置（利用 `For ... Each` 命令）。

## 定义自定类型

使用 `Type` 关键字定义自定类型，例如：

```basic
Type MyType 
    Field x, y 
End Type
```

这将创建一个名为 `MyType` 的自定类型，其中包括两个字段：`x` 和 `y`。

自定类型的字段可以是任意基本数据类型，也可以是任意自定类型。类型标签可以用于确定字段的类型，例如：

```basic
Type MyType 
    Field x, y               ; 整数值
    Field description$       ; 字符串 
    Field delta_x#, delta_y# ; 浮点值
End Type 
```

## 创建自定类型实例

您可以在创建变量或数组的名称之后用 “`.`+类型名称”的方式创建自定类型的变量或数组。例如：

```basic
Global mine.MyType
Dim all_mine.MyType(100)
```

在使用自定类型变量或数组元素之前，必须使用 `New` 运算符对其进行初始化。例如：

```basic
mine.MyType = New MyType
```

`New` 运算符将创建一个类型为 MyType 的“对象”，并返回创建的对象的“指针”。`New` 运算符后面的标识符必须是有效的自定类型名称。

自定类型中的字段可以通过“`\`”字符访问。例如：

```basic
mine\x=100
Print mine\x
```

## 销毁自定类型实例

当您不再需要一个对象的时候，您应该使用 `Delete` 命令将其删除。例如：

```basic
Delete mine
```

这将释放对象所使用的内存。

## 检测是否存在

特殊关键字 `Null` 被用于表示不存在的对象。如果对象尚未用 `New` 进行初始化，或者已被 `Delete` 进行删除，则该对象不存在。例如：

```basic
mine.MyType = New MyType 
If mine <> Null 
     Print "exists!" ; 存在！
Else 
     Print "doesn't exist!" ; 不存在！
EndIf 
Delete mine 
If mine <> Null 
     Print "exists!" ; 存在！
Else 
     Print "doesn't exist!" ; 不存在！
EndIf 
```

...就会打印：

```
exists! 
doesn't exist!
```

每个自定类型都有一个属于自己的对象列表，称为“类型列表”。使用 `New` 创建对象时，创建的对象将自动添加到类型列表中。使用 `Delete` 释放对象时，对象将从列表中移除。类型列表是动态的——一旦实例被销毁，它在集合中就会被删除，其他的对象就会在集合中“上移”。

## 类型列表迭代

`First`、`Last`、`After` 和 `Before` 运算符允许您访问类型列表。`First` 运算符会返回类型列表开头的对象。例如：

```basic
mine.MyType = First MyType
```

这将为 `mine.MyType` 赋值自定类型 MyType 的类型列表中的第一个对象。

同理，`Last` 会返回列表末尾的对象。

如果类型列表为空，则 `First` 和 `Last` 将会返回 `Null`。

您可以使用 `After` 查找一个对象之后的对象，使用 `Before` 查找一个对象之前的对象。例如：

```basic
mine.MyType = First MyType ; mine=类型列表的第一个对象
mine = After(mine) ; mine=第二个对象
mine = After(mine) ; mine=第三个对象
mine = Before(mine) ; mine=第二个对象
mine = Before(mine) ; mine=又是第一个！
```

如果类型列表中找不到对象，`After` 和 `Before` 将返回 `Null`。例如：

```basic
mine.MyType = Last MyType ; mine=最后一个对象
mine = After(mine) ; 最后一个后面没有对象！
```

使用 `New` 创建对象时，默认情况下，该对象将会放置在其类型列表的末尾。然而，您可以使用 `Insert` 来在类型列表中移动对象。

```basic
mine1.MyType = New MyType
mine2.MyType = New MyType 
Insert mine2 Before mine1
```

这将会把 `mine2` 对象插入 `mine1` 之前。您也可以使用 `After` 在其之后插入，而不是用 `Before`。

以下是将对象移动到类型列表开头的示例：

```basic
Insert mine Before First MyType
```

一种特殊形式的 `For ... Next` 允许您轻松遍历列表中的所有对象。例如：

```basic
For mine.MyType = Each MyType 
    ...
Next
```

这会让变量 `mine.MyType` 循环赋值为 MyType 列表中的所有对象。

最后，`Delete Each` 命令允许您删除特定类型列表中的所有对象。例如：

```basic
Delete Each MyType
```
