---
tags: []
date: 2026-01-25
time: 22:15
---


## ReferenceError vs TypeError 的區別

| 情況                             | 錯誤類型               |
| ------------------------------ | ------------------ |
| 變數根本不存在                        | **ReferenceError** |
| 變數存在但值是 undefined/null，然後存取其屬性 | **TypeError**      |

```javascript
// ReferenceError - 變數不存在
foo.name;  // ReferenceError: foo is not defined

// TypeError - 變數存在，但值無法存取屬性
let foo = undefined;
foo.name;  // TypeError: Cannot read properties of undefined
```