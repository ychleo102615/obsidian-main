---
tags: []
date: 2026-05-19
time: 00:00
---

## Portrait Reveal
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



## Ripple Buttons

這題中我卡到的一個地方是，我以為 `transform-origin: center` 可以把錨點移到中心。但是實際上這邊還是都用 `translate: -50% -50%` 來處理。