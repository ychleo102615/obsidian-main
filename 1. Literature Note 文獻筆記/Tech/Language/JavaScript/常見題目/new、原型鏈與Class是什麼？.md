---
tags: []
date: 2026-01-25
time: 17:42
link: https://brucefe.com/zh-tw/frontend-interview-prepare/new-prototype-class
---

## 原型鏈


| `Function`      | `Object`    |
| --------------- | ----------- |
| `prototype`<br> | `__proto__` |

```js
function Dog(name) {
	this.name = name
}

Dog.prototype.bark = function() {
	console.log( `${this.name} says woof!`)
}

const dog1 = new Dog('dog1')
```