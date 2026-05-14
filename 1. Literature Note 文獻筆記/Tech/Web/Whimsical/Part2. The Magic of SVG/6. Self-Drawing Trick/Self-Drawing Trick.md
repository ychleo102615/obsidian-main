---
tags: []
date: 2026-05-14
time: 16:57
---
[[Strokes and Fills#Dashes]]
`stroke-dasharray`
建立超大的 gap，並且漸漸增加 dash 的長度。

但是 dash 的長度即使是 0 ，也會渲染 linecap。

使用 offset。

## Getting the path length programmatically

檢查 path 的長度：
```js
const elem = document.querySelector('path');
const pathLength = elem.getTotalLength();
console.log(pathLength); // 365.54931640625
```

## Setting a custom scale with the pathLength property

比起手算長度，可以自行設定長度比例尺。
```css
<path
  pathLength="100"
  ...
>
```
之後內部的 px 單位都要參照比