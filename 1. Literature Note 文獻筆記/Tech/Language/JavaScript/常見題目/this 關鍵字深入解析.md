---
tags: []
date: 2026-01-25
time: 21:31
---


### 五種綁定規則
- `預設綁定`：this 指向全域或是 undefined （非嚴格/嚴格模式）
- 隱含綁定：作為物件方法調用時，this 指向該方法的物件
- 顯示綁定：使用 `call()`, `apply()`, `bind()` 明確指定 this 的值
- `new` 綁定：使用 new 關鍵字調用函式時，this 只