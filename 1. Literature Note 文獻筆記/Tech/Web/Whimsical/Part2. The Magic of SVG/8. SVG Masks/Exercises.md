---
tags: []
date: 2026-05-15
time: 16:38
---

## Filling Heart

疑問：SVG 圖形要怎麼取得寬高？尤其是 path？
解答是硬算的。

實際上是有的：
```js
const path = document.querySelector('path');
const bbox = path.getBBox();

console.log(bbox.width);  // 寬
console.log(bbox.height); // 高
console.log(bbox.x);      // 左上角 x
console.log(bbox.y);      // 左上角 y
```

[utilities](https://courses.joshwcomeau.com/wham/01-particles/10.02-lerp-utils)  用指數來建立進度會更像真的填滿體積和更快取得回饋。

