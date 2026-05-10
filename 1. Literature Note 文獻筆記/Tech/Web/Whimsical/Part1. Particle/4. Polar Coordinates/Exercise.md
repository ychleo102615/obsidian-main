---
tags: []
date: 2026-05-10
time: 20:35
link: https://courses.joshwcomeau.com/wham/01-particles/07.02-polar-exercises
---

# Rocketship
這個題目要在火箭的尾部生成一個持續發散粒子的動畫。

為了把粒子產生的點黏在火箭尾部上，我想到的方式是計算火箭本身（他有在跑 oscillate transform  動畫）的 rect 對應到全域的位置上（body）。

講師的解法比較簡單。他的粒子 parent 仍然在火箭的 wrapper 元件上，但是就不考慮 spawn 位置要跟隨火箭移動的問題了：
```css
.particle {
	left: 0;
	right: 0;
	bottom: 20px;
	margin-inline: auto;
}
```
這個技巧也在 [[Alternative Approach]] 中出現。