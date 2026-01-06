---
tags: []
date: 2026-01-06
time: 13:19
link: https://www.explainthis.io/zh-hant/swe/es6
---

ES6（也稱為 ES2015）是一個里程碑式的版本，引入了許多期待已久的語法糖和新特性。這些新增功能大大提升了開發者的編程體驗和效率。

# 1. let & const

理解為什麼不用 `var`，首先要看它們在作用域和行為上的本質區別：

| 特性                  | `var`                  | `let` / `const`          |
| ------------------- | ---------------------- | ------------------------ |
| **作用域**             | 函式作用域 (Function Scope) | 區塊作用域 (Block Scope `{}`) |
| **變數提升 (Hoisting)** | 會提升並初始化為 `undefined`   | 會提升但存在「暫時性死區」(TDZ)       |
| **重複宣告**            | 允許在同一作用域重複宣告           | 不允許，會拋出錯誤                |
| **全域屬性**            | 在全域宣告時會成為 `window` 的屬性 | 不會成為 `window` 的屬性        |
# 2. Arrow Function

1. 沒有 this
2. 沒有 arguments
3. 不能當作 constructor
# 3. Template Literals
# 4. Destructing Assignment
# 5. Default Parameter
# 6. Spread Operator & Rest Parameter
# 7. Class
constructor 的語法糖
# 8. Modules
# 9. Promise