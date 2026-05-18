---
tags: []
date: 2026-05-19
time: 00:00
---

這個作業中，我忘記考慮不是滑鼠的狀態，還有只使用 keyboard 的狀態（focus）

```css
.wrapper:focus .fellow {
    filter: blur(0px);
    transform: translateY(0px);
}
```

```css
@media not (pointer: fine | coarse | none) {
}
```