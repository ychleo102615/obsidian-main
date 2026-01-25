---
tags: []
date: 2026-01-25
time: 17:42
link: https://brucefe.com/zh-tw/frontend-interview-prepare/new-prototype-class
---

## 原型鏈

### `__proto__` 與 `prototype`

JavaScript 物件系統是基於原型的，有兩個關鍵概念：
- `prototype`: 是函式的屬性，包含將被共享給實例的方法與屬性
- `__proto__`: 是物件的屬性，指向建立該物件的構造函式的 prototype

| `Function`      | `Object`    |
| --------------- | ----------- |
| `prototype`<br> | `__proto__` |

```js
function Dog(name) {
	this.name = name
}

Dog.prototype.bark = function() {
	console.log(`${this.name} says woof!`)
}

const dog1 = new Dog('dog1');
dog1.bark();

console.log(dog1.__proto__ === Dog.prototype) // true
```


### 代替 `__proto__` 的方法

```js
Object.getPrototypeOf(obj) // obj.__proto__

Object.setPrototypeOf(obj, prototype)// obj.__proto__ = prototype

// 創建帶有指定圓形的新物件
Object.create(prototype) // 比 new 更直接
```


### 私有變數

##### ES2022
```js
class BankAccount {
	#balance = 0 // Private field
}
```

### 常見面試題目

#### 1. new 關鍵字做了什麼
1. 建立新的空物件
2. 指定物件 `__proto__` 屬性為函式 `prototype` 屬性
3. 綁定 this
4. 執行函式
5. 如果函式沒有返回對象，回傳新創建的物件

```js
function myNew(Constructor, ...args) {
	let obj = Object.create(Constructor)

	// 錯誤，沒有綁定
	// let ret = Constructor(args)
	
	// 執行構造函數，並將 this 指向新創建的物件
	let ret = Constructor.apply(ret, args)
	
	return ret instanceof Object ? ret : obj
}
```

#### 2. `prorotype` 和 `__proto` 的差異

### 3. ES6 的 Class 和傳統建構函數有何不同

class 只是語法糖，本質沒有變。

| 比較項目     | Class 寫法         | Function 寫法    |
| -------- | ---------------- | -------------- |
| **語法**   | 更清晰直觀，OOP風格      | 較為分散，需分別定義原型方法 |
| **提升行為** | **不會被提升**        | 函式聲明會被提升       |
| **繼承實現** | 使用 extends 關鍵字簡潔 | 需手動設置原型鏈，較複雜   |
| **靜態方法** | 使用 static 關鍵字定義  | 直接賦值給構造函式      |
| **私有屬性** | 支持 # 語法定義真正私有屬性  | 需使用閉包或其他技巧模擬   |
| **兼容性**  | ES6+，需考慮舊瀏覽器兼容   | 全面支持，兼容性好      |
