---
tags: []
date: 2026-05-15
time: 15:34
link: https://courses.joshwcomeau.com/wham/02-svg/09-transforms-in-svg
---
SVG 讓圖案旋轉要考慮 transform origin 問題。
之前的練習我也有遇過這過坑：
- [[1. Literature Note 文獻筆記/Tech/Web/Whimsical/Part2. The Magic of SVG/6. Self-Drawing Trick/Exercise#Circular Progress Indicator|6. Self-Drawing Trick/Exercise#Circular Progress Indicator]]
- [[1. Literature Note 文獻筆記/Tech/Web/Whimsical/Part2. The Magic of SVG/4. SVG Animations/Exercise|4. SVG Animations/Exercise]]

但 SVG 的中心會在整個圖形的中心。

## The fix
使用該繪圖指令原本的位移：
```html
<style>
    text {
        transform: rotate(-1deg);
        transform-origin: 150px 100px;
    }
</style>
<svg viewBox="0 0 250 250">
    <text x="150" y="100">
        Hello
    </text>
</svg>
```

