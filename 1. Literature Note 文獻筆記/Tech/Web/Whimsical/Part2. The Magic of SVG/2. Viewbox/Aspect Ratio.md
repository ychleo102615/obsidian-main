---
tags: []
date: 2026-05-14
time: 11:46
---
當 SVG width/height 不等於 viewBox 的 ratio 時，會發生什麼事？

預設的情況下，SVG 不會被拉伸。
ratio 不同時，會在上下或是左右方向留空。

想要拉伸的時候：
```css
<svg
    viewBox="0 0 1440 300"
    preserveAspectRa
>
```