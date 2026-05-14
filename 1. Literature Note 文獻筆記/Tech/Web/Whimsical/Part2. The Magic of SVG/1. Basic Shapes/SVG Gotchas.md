---
tags: []
date: 2026-05-14
time: 11:06
---

## Stacking Order
SVG 沒有 z-index 效果。

## Dynamically-created elements

我們無法用傳統建立 HTML element 的方式建立 SVG element。

```js
// 無效
const circle = document.createElement('circle');

// 有效
const circle = document.createElementNS(
    'http://www.w3.org/2000/svg',
    'circle'
);
```

`NS` 代表 `XML namespace`，包含：
- `http://www.w3.org/1999/xhtml`
- `http://www.w3.org/2000/svg`
- `http://www.w3.org/1998/Math/MathML`


HTML5 以前，需要使用 `xmlns` 來聲明 SVG。之後