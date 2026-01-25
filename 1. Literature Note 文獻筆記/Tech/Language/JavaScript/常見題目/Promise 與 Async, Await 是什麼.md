---
tags: []
date: 2026-01-26
time: 00:07
link: https://brucefe.com/zh-tw/frontend-interview-prepare/promise-async-await
---



### 考題

### 狀態轉換的規則是什麼
- 同時只有一種狀態（pending, fulfilled, rejected）
- 初始狀態為 pending
- 只能從 pending 轉到 fulfilled, rejected
- 不可逆
- 切換時觸發對應的 callback

### all, race 區別





```js
async function example() {
	return "Hello"
}
// 等價於
function example() {
	return Promise.resolve("Hello")
}
```