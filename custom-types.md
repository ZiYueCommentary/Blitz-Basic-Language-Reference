# 自定型別

### 什麼是自定型別？ <a href="#what-are-they" id="what-are-they"></a>

**自定型別是你最好的朋友。**它被用於建立擁有相同引數的物件的“集合”，並且快速輕鬆地進行互動。

> 想象一下《太空入侵者》，現在螢幕上有很多的外星人。每一個外星人都有一些需要的變數：x、y 和一個控制畫面顯示的變數（腿向外或向內）。
>
> 現在，我們可以建立數百個變數，例如 `invader1x`、`invader1y`、`invader2x`、`invader2y` 來控制所有的外星人。但是這沒多大意義，不是嗎？你可以用陣列來儲存它們，並且使用 `For ... Next` 迴圈，但是這太麻煩了！
>
> “自定型別變數集合”就是用來解決這種問題的。

`Type` 能夠定義一個物件集合。每個物件都會獲得型別中 `Field` 定義的變數的副本。集合中每個物件的每個變數都可以單獨讀取，並且可以快速迭代。使用 `Field` 命令在 `Type` 和 `End Type` 中間定義所需的變數。

如果有幫助的話，您可以將型別集合想象成一個數據庫。每個物件都是資料庫的記錄，每個變數都是記錄中的欄位。使用 `Before`、`After` 和 `For ... Each` 命令，您可以移動“資料庫”的指標來指向不同的記錄，以檢索並設定變數的欄位值。

> 不是資料庫專家？還需要舉個例子？沒問題。想象你正在為一場演講或一次活動搭建場景，你將要為觀眾擺數百把椅子。
>
> 椅子必須要放在地板上的某個地方，而有些椅子會比其他椅子高一點（比如老闆和市長的椅子）。所以，作為電腦天才，你正在想辦法最快最好地來佈置椅子。
>
> 你意識到地板是方格的，地板完全是一個巨大的網格！弄這事更簡單了！你只需要在一張圖紙上對地板進行編號，並根據老闆告訴你的重要人物的座位，將每張椅子的高度寫到網格表上。
>
> 所以，每把椅子有會有一個 x 和 y，並會有一個水平高度來表示椅子的高度（height）。很好，我們邏輯很清晰。現在，儘管我們把這些東西都寫在圖紙上了，我們仍舊需要自己去放椅子。
>
> 當你完成之後，你的老闆走到你面前說：“它們沒有居中，把它們向右平移一米。”我操！本來這些東西都很完美。儘管椅子右移一米這事不難（畢竟它們的高度和順序不會改變），但是你仍舊要一把一把挪這些椅子！
>
> 如果你能揮揮手說：“房間裡的椅子的 x 都增加一個方格”，然後它們奇蹟的挪過去了，那就太棒了。但是現實是——這些椅子都要你自己搬！

在 Blitz 中，你可以設定一個叫做 `Chair` 的型別，然後將型別的欄位（Field）設定為 `x`、`y` 和 `height`。您可以使用 `New` 命令來建立所需數量的椅子（每次呼叫 `New` 時，它都會生成一把帶有屬於自己的 `x`、`y` 和 `height` 的新的椅子），併為他們分配由您決定的 `x`、`y` 和 `height`。

在上面的例子中，當老闆讓你把椅子挪動一格的時候，你可能會叫苦連天——這活可不少！但是在 Blitz 中，我們可以用四行程式碼讓所有的 `Chair` 物件調整到新位置（利用 `For ... Each` 命令）。

### 定義自定型別 <a href="#defining-a-type" id="defining-a-type"></a>

使用 `Type` 關鍵字定義自定型別，例如：

```basic
Type MyType 
    Field x, y 
End Type
```

這將建立一個名為 `MyType` 的自定型別，其中包括兩個欄位：`x` 和 `y`。

自定型別的欄位可以是任意基本資料型別，也可以是任意自定型別。型別標籤可以用於確定欄位的型別，例如：

```basic
Type MyType 
    Field x, y               ; 整數值
    Field description$       ; 字串 
    Field delta_x#, delta_y# ; 浮點值
End Type 
```

### 建立自定型別例項 <a href="#creating-a-type-instance" id="creating-a-type-instance"></a>

您可以在建立變數或陣列的名稱之後用 “`.`+型別名稱”的方式建立自定型別的變數或陣列。例如：

```basic
Global mine.MyType
Dim all_mine.MyType(100)
```

在使用自定型別變數或陣列元素之前，必須使用 `New` 運算子對其進行初始化。例如：

```basic
mine.MyType = New MyType
```

`New` 運算子將建立一個型別為 MyType 的“物件”，並返回建立的物件的“指標”。`New` 運算子後面的識別符號必須是有效的自定型別名稱。

自定型別中的欄位可以透過“`\`”字元訪問。例如：

```basic
mine\x=100
Print mine\x
```

### 銷燬自定型別例項 <a href="#destroying-a-type-instance" id="destroying-a-type-instance"></a>

當您不再需要一個物件的時候，您應該使用 `Delete` 命令將其刪除。例如：

```basic
Delete mine
```

這將釋放物件所使用的記憶體。

### 檢測是否存在 <a href="#determining-existance" id="determining-existance"></a>

特殊關鍵字 `Null` 被用於表示不存在的物件。如果物件尚未用 `New` 進行初始化，或者已被 `Delete` 進行刪除，則該物件不存在。例如：

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

...就會列印：

```
exists! 
doesn't exist!
```

每個自定型別都有一個屬於自己的物件列表，稱為“型別列表”。使用 `New` 建立物件時，建立的物件將自動新增到型別列表中。使用 `Delete` 釋放物件時，物件將從列表中移除。型別列表是動態的——一旦例項被銷燬，它在集合中就會被刪除，其他的物件就會在集合中“上移”。

### 型別列表迭代 <a href="#iteration-through-type-lists" id="iteration-through-type-lists"></a>

`First`、`Last`、`After` 和 `Before` 運算子允許您訪問型別列表。`First` 運算子會返回型別列表開頭的物件。例如：

```basic
mine.MyType = First MyType
```

這將為 `mine.MyType` 賦值自定型別 MyType 的型別列表中的第一個物件。

同理，`Last` 會返回列表末尾的物件。

如果型別列表為空，則 `First` 和 `Last` 將會返回 `Null`。

您可以使用 `After` 查詢一個物件之後的物件，使用 `Before` 查詢一個物件之前的物件。例如：

```basic
mine.MyType = First MyType ; mine=型別列表的第一個物件
mine = After(mine) ; mine=第二個物件
mine = After(mine) ; mine=第三個物件
mine = Before(mine) ; mine=第二個物件
mine = Before(mine) ; mine=又是第一個！
```

如果型別列表中找不到物件，`After` 和 `Before` 將返回 `Null`。例如：

```basic
mine.MyType = Last MyType ; mine=最後一個物件
mine = After(mine) ; 最後一個後面沒有物件！
```

使用 `New` 建立物件時，預設情況下，該物件將會放置在其型別列表的末尾。然而，您可以使用 `Insert` 來在型別列表中移動物件。

```basic
mine1.MyType = New MyType
mine2.MyType = New MyType 
Insert mine2 Before mine1
```

這將會把 `mine2` 物件插入 `mine1` 之前。您也可以使用 `After` 在其之後插入，而不是用 `Before`。

以下是將物件移動到型別列表開頭的示例：

```basic
Insert mine Before First MyType
```

一種特殊形式的 `For ... Next` 允許您輕鬆遍歷列表中的所有物件。例如：

```basic
For mine.MyType = Each MyType 
    ...
Next
```

這會讓變數 `mine.MyType` 迴圈賦值為 MyType 列表中的所有物件。

最後，`Delete Each` 命令允許您刪除特定型別列表中的所有物件。例如：

```basic
Delete Each MyType
```
