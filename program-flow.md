# 程序流

以下结构可用于控制程序流。

## If ... Then

```basic
If {表达式} Then {语句1} Else {语句2} 
```

如果 `If` 表达式结果为真，则执行 `Then` 的 `{语句1}`，如果结果为假，则执行 `Else` 的 `{语句2}`。`Else` 部分是可省略的，其语句范围为 `Else` 到行尾。

```basic
If {表达式1}
     {语句1} 
Else If {表达式2}
     {语句2} 
Else If {表达式3}
     {语句3}
Else 
     {语句4} 
EndIf
```

`If` 语句的这种形式允许存在多行语句。`Else If` 和 `Else` 部分是可选的。当 `If` 和 `Else If` 都不为真时才会执行 `Else` 语句。

## While ... Wend

```basic
While {表达式} 
     {语句} 
Wend
```

`While` 循环语句将一致循环执行，直到 `{表达式}` 的结果为假。`{表达式}` 将在每个循环开始前求值。

## For ... Next

```basic
For {变量}={初始值} To {结束值} Step {步进} 
     {语句} 
Next 
```

`For/Next` 循环将在循环开始前将 `{初始值}` 复制给 `{变量}`，然后再开始循环。循环将一直进行到 `{变量}` 等于 `{结束值}` 时，值 `{步进}` 将被加入 `{变量}` 中。如果没有指定步进值，则步进值默认为 `1`。

这种形式的 `For/Next` 循环将允许您迭代自定类型的所有对象。

## Repeat ... Until/Forever

```basic
Repeat 
     {语句} 
Until {表达式}
```

`Repeat` 循环将一直执行，直到 `{表达式}` 的结果为真。`{表达式}` 将在每个循环结束时求值。

```basic
Repeat 
     {语句} 
Forever
```

`Repeat/Forever` 循环将不断执行 `{语句}`，直到程序结束或执行 `Exit` 命令。

## Select ... Case

```basic
Select {表达式} 
     Case {表达式1}
          {语句1} 
     Case {表达式2} 
          {语句2}
     Default 
          {语句3} 
End Select 
```

`Select` 语句将首先计算 `{表达式}`，然后将其与 `Case` 的表达式进行比较，如果其数据与 `Case` 匹配，则执行 `Case` 中的语句。

如果 Select 表达式中的所有 Case 都不匹配的话，则执行可选的 `Default` 中的语句。

## 退出循环 <a href="#breaking-out-of-a-loop" id="breaking-out-of-a-loop"></a>

`Exit` 命令可以用于中断任何 `For ... Next`、`While ... Wend`、`Repeat ... Until` 或 `Repeat ... Forever` 循环。

## 导入文件 <a href="#using-includes" id="using-includes"></a>

Blitz 还支持 `Include` 命令。Include 命令允许将其他源文件导入当前源文件，作为主程序的一部分。Include 命令后必须跟随一个被引号包括起来的文件名。例如：

```basic
Include "另一个文件.bb"
```

Include 允许您将程序划分为更小、更易于管理的区块。
