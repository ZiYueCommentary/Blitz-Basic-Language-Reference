# 程式流

以下結構可用於控制程式流。

### If ... Then

```basic
If {表示式} Then {語句1} Else {語句2} 
```

如果 `If` 表示式結果為真，則執行 `Then` 的 `{語句1}`，如果結果為假，則執行 `Else` 的 `{語句2}`。`Else` 部分是可省略的，其語句範圍為 `Else` 到行尾。

```basic
If {表示式1}
     {語句1} 
Else If {表示式2}
     {語句2} 
Else If {表示式3}
     {語句3}
Else 
     {語句4} 
EndIf
```

`If` 語句的這種形式允許存在多行語句。`Else If` 和 `Else` 部分是可選的。當 `If` 和 `Else If` 都不為真時才會執行 `Else` 語句。

### While ... Wend

```basic
While {表示式} 
     {語句} 
Wend
```

`While` 迴圈語句將一致迴圈執行，直到 `{表示式}` 的結果為假。`{表示式}` 將在每個迴圈開始前求值。

### For ... Next

```basic
For {變數}={初始值} To {結束值} Step {步進} 
     {語句} 
Next 
```

`For/Next` 迴圈將在迴圈開始前將 `{初始值}` 複製給 `{變數}`，然後再開始迴圈。迴圈將一直進行到 `{變數}` 等於 `{結束值}` 時，值 `{步進}` 將被加入 `{變數}` 中。如果沒有指定步進值，則步進值預設為 `1`。

這種形式的 `For/Next` 迴圈將允許您迭代自定型別的所有物件。

### Repeat ... Until/Forever

```basic
Repeat 
     {語句} 
Until {表示式}
```

`Repeat` 迴圈將一直執行，直到 `{表示式}` 的結果為真。`{表示式}` 將在每個迴圈結束時求值。

```basic
Repeat 
     {語句} 
Forever
```

`Repeat/Forever` 迴圈將不斷執行 `{語句}`，直到程式結束或執行 `Exit` 命令。

### Select ... Case

```basic
Select {表示式} 
     Case {表示式1}
          {語句1} 
     Case {表示式2} 
          {語句2}
     Default 
          {語句3} 
End Select 
```

`Select` 語句將首先計算 `{表示式}`，然後將其與 `Case` 的表示式進行比較，如果其資料與 `Case` 匹配，則執行 `Case` 中的語句。

如果 Select 表示式中的所有 Case 都不匹配的話，則執行可選的 `Default` 中的語句。

### 退出迴圈 <a href="#breaking-out-of-a-loop" id="breaking-out-of-a-loop"></a>

`Exit` 命令可以用於中斷任何 `For ... Next`、`While ... Wend`、`Repeat ... Until` 或 `Repeat ... Forever` 迴圈。

### 匯入檔案 <a href="#using-includes" id="using-includes"></a>

Blitz 還支援 `Include` 命令。Include 命令允許將其他原始檔匯入當前原始檔，作為主程式的一部分。Include 命令後必須跟隨一個被引號包括起來的檔名。例如：

```basic
Include "另一個檔案.bb"
```

Include 允許您將程式劃分為更小、更易於管理的區塊。
