[中文](https://maxleebk.com/2020/07/25/prototype/)
[stackoverflow](https://stackoverflow.com/questions/38740610/object-getprototypeof-vs-prototype)

[![](https://maxleebk.com/2020/07/25/prototype/chain.png)](https://maxleebk.com/2020/07/25/prototype/chain.png)






# Very Notatble
---
## new 運算子

現在知道當我們在創建實例時，主要會有兩件事情發生：

-   **實例會被初始化，並透過建構函式新增屬性**
-   **實例的 `__proto__` 會被指向建構函式的 `prototype`**

但這些事情怎麼發生的？而且為什麼在 `Car` 裡面使用 `this` 會是幫實例加上屬性呢？  
正常來說函式中的 `this` 指向的應該會是 `window`，所以要是你直接執行 `Car` 的話，應該是 `window` 會被設定屬性才對：

```javascript
Car(1, 1, "空氣");
console.log(window.door); // 1
```

其實一切的關鍵都在於 `new`，我們可以用函式來模擬 `new` 做的事情：

```javascript
function newObject(Constructor, arguments) {
  var o = new Object();  // 1. 建立新物件
  o.__proto__ = Constructor.prototype;  // 2. 重新指向原型
  Constructor.apply(o, arguments);  // 3. 初始化物件
  return o; // 4. 回傳新物件
};
let truck = newObject(Car, [6, 2, "柴油"]);
```

  

1.  **建立新物件：** 建立一個新物件，起初這個物件的 `__proto__` 指向的會是 `Object.prototype`
2.  **重新指向原型：** 重新將 `__proto__` 指向建構函式的原型，使物件成為建構函式的實例
3.  **初始化物件：** 執行建構函式，但利用 `apply` 將 `this` 指定給實例，這樣才能為它新增屬性
4.  **回傳新物件：** 最後回傳這個處理完成的實例

`new` 背後做的事情不是很複雜但卻很重要，它將實例以及原型之間建立了連結。