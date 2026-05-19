---
tags: []
date: 2026-05-19
time: 13:16
---

獲取 bounding box 的方法：
# `.getBoundingClientRect()`

但是呼叫的時候， js engine 需要分析 DOM。如果每次移動滑鼠、捲動滾軸都要更新計算的話，會影響效能。

## Measuring when the environment changes
即使在必要的時候才更新，仍可能被觸發多次：
```js
function handleUpdate() {
  console.log('Recalculating bounding box', Date.now());
  boundingBox = socket.getBoundingClientRect();
}
window.addEventListener('scroll', handleUpdate);
window.addEventListener('resize', handleUpdate);

```

## Throttling to the rescue