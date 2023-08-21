# 函式

函式使用 `Function` 關鍵字定義：

```basic
Function {函式名}{型別標籤}({引數}) 
     {語句} 
End Function
```

* `{函式名}` 可以是任意有效識別符號。
* `{型別標籤}` 是函式返回值的型別。如果 `{型別標籤}` 被忽略，則函式預設返回整數值。
* `{引數}` 是一個用逗號分割開來的變數列表，在呼叫函式時將資料傳遞給函式。每個引數有可以有一個獨立的型別標籤。引數永遠為本地變數。

函式可以使用 `Return` 語句返回結果。`Return` 後面可以是表示式。

如果函式沒有 `Return` 語句，或者函式使用了不帶任何表示式的 `Return`，則整數值函式將預設返回 `0`，字串函式預設返回 `""`，自定型別值函式返回 `Null` 物件。