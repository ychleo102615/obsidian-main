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

```js
class BankAccount {
#}
```