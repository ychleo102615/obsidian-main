---
tags: []
date: 2026-05-14
time: 16:57
---
[[Strokes and Fills#Dashes]]
`stroke-dasharray`
建立超大的 gap，並且漸漸增加 dash 的長度。

檢查 path 的長度：
```js
const path = document.querySelector('.path');
const length = path.getTotalLength();
```

但是 dash 的長度即使是 0 ，也會渲染 linecap。

使用 offset。