---
tags: []
date: 2026-01-25
time: 21:31
---


### 五種綁定規則
- 預設綁定：this 指向全域或是 undefined （非嚴格/嚴格模式）
- 隱含綁定：作為物件方法調用時，this 指向該方法的物件
- 顯示綁定：使用 `call()`, `apply()`, `bind()` 明確指定 this 的值
- `new` 綁定：使用 new 關鍵字調用函式時，this 指向新建立的物件
- 箭頭函式綁定：箭頭函式沒有自己的 this，使用外層作用域的 this


##### 顯示綁定
call 跟 apply 幾乎一樣，差別在參數給予的方式。
bind 回傳包裝好的函式。 

哪些狀況適合使用 bind？



### 題目

##### 箭頭函式

```js
const obj = {
  name: "Leo",
  greet: () => {
    console.log(this.name);
  }
};

obj.greet();
```

 輸出什麼？
 
---

```js
obj.greet();  // "" 或 undefined，不是 "Leo"
```

**關鍵：箭頭函式沒有自己的 `this`，捕捉的是「定義時」外層作用域的 `this`。**

物件字面量 `{}` **不會創建作用域**，所以這個箭頭函式定義在全域，`this` 是全域物件。


##### 巢狀函式

```js
const obj = {
  name: "Leo",
  greet: function() {
    function inner() {
      console.log(this.name);
    }
    inner();
  }
};

obj.greet();
```

輸出什麼？

---


```js
inner();  // "" 或 TypeError，不是 "Leo"
```

**`inner()` 是獨立調用**，不是 `obj.inner()`，所以 `this` 不是 `obj`。

這是經典陷阱：**巢狀在方法裡的普通函式，`this` 不會繼承外層。**

##### setTimeout

```js
const obj = {
  name: "Leo",
  greet: function() {
    setTimeout(function() {
      console.log(this.name);
    }, 100);
  }
};

obj.greet();
```

輸出什麼？如果要讓它正確印出 `"Leo"`，有哪些改法？

---


```js
// 改法 1：箭頭函式
setTimeout(() => {
  console.log(this.name);
}, 100);

// 改法 2：bind
setTimeout(function() {
  console.log(this.name);
}.bind(this), 100);

// 改法 3：保存 this
const self = this;
setTimeout(function() {
  console.log(self.name);
}, 100);
```


##### bind 陷阱

```js
const obj = {
  name: "Leo"
};

function greet() {
  console.log(this.name);
}

const bound = greet.bind(obj);
const bound2 = bound.bind({ name: "Alice" });

bound2();
```

---

```js
bound2();  // "Leo"，不是 "Alice"
```

**`bind` 只能綁定一次，後續再 `bind` 無效。**

這是 `bind` 的特性：回傳的函式 `this` 已經被「鎖死」，無法再被 `bind` / `call` / `apply` 改變。