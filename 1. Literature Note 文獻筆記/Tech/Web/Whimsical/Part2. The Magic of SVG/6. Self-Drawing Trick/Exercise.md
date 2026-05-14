---
tags: []
date: 2026-05-14
time: 17:49
link: https://courses.joshwcomeau.com/wham/02-svg/07.01-self-drawing-exercises
---
## Self-drawing swoop

```css
.foreground {
    stroke-dasharray: 100, 1000;
    stroke-dashoffset: 100px;
}
button:hover .foreground {
    stroke-dashoffset: 0px;
}
@media (prefers-reduced-motion: no-preference) {
    .foreground {
        transition: stroke-dashoffset 750ms;
    }
}
```

我最初還想要使用 `button.addEventListener('mouseover)`
來操作，並且用 keyframes。

但是就功能語意上來說，用 keyframes 完全不適合（應該說用起來會太麻煩）。
這裡的動畫涉及狀態切換，適合使用 transition。


## Circular Progress Indicator

pageLength 雖然是 presentation attribute ，但是他無勇