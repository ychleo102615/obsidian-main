---
tags: []
date: 2026-05-14
time: 10:56
---

Text 也可以套用 fill, stroke。

```css
text {
    paint-order: stroke fill;
}
```
通常 stroke 會在 fill 之後繪製。此設定可以調整順序，達到不一樣的效果。

同樣的效果也可以應用在 HTML 上。
```css
h1 {
    -webkit-text-stroke: 6px hotpink;
    color: var(--page-bg-color);
    paint-order: stroke fill;
}
```