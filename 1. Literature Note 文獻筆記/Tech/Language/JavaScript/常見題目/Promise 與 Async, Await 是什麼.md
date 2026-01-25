---
tags: []
date: 2026-01-26
time: 00:07
link: https://brucefe.com/zh-tw/frontend-interview-prepare/promise-async-await
---

## 為何需要 Promise？Why Do We Need Promises?

#####  Promise 解決了傳統回調函式的多個問題，提供了更優雅的非同步處理方式：
 
- `避免回調地獄`：解決巢狀回調導致的程式碼難以維護問題
`Avoiding callback hell`: Solves code maintainability issues caused by nested callbacks
- `統一錯誤處理`：使用 catch 方法統一處理錯誤
`Unified error handling`: Using the catch method to handle errors uniformly
- `鏈式調用`：通過 then 方法實現清晰的流程控制
`Chaining`: Implementing clear flow control through the then method
- `更好的語義化`：Promise 的狀態轉換更符合程式設計直覺
`Better semantics`: Promise state transitions are more intuitive for programming


### 考題

### 狀態轉換的規則是什麼
- 同時只有一種狀態（pending, fulfilled, rejected）
- 初始狀態為 pending
- 只能從 pending 轉到 fulfilled, rejected
- 不可逆
- 切換時觸發對應的 callback

## Promise 的靜態方法Promise Static Methods

#### Promise.all()

並行執行多個 Promise，等待全部完成。如果任一 Promise 失敗，整個操作就失敗。Executes multiple Promises in parallel, waiting for all to complete. If any Promise fails, the entire operation fails.

```javascript
Promise.all([
  fetch('/api/users'),
  fetch('/api/posts')
]).then(([users, posts]) => {
  // process results
});
```

#### Promise.race()

返回最先完成的 Promise 結果，無論成功或失敗。Returns the result of the first completed Promise, regardless of success or failure.

```javascript
Promise.race([
  fetch('/api/data'),
  new Promise((_, reject) =>
    setTimeout(() => reject('Timeout'), 5000)
  )
]);
```

#### Promise.any()

返回第一個成功的 Promise 結果，只有全部失敗時才會拒絕。Returns the result of the first successful Promise. Only rejects when all Promises fail.

```javascript
Promise.any([
  fetch('https://api1.example.com'),
  fetch('https://api2.example.com')
]).then(firstSuccess => {
  // Handle the first successful result
});
```

#### Promise.allSettled()

等待所有 Promise 完成，返回每個 Promise 的結果狀態。Waits for all Promises to complete, returning the status of each Promise result.

```javascript
Promise.allSettled([
  fetch('/api/users'),
  fetch('/api/posts')
]).then(results => {
  // process all results
});
```




### 語法糖

```js
async function example() {
	return "Hello"
}
// 等價於
function example() {
	return Promise.resolve("Hello")
}
```