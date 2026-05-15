---
tags: []
date: 2026-05-14
time: 14:48
link: https://courses.joshwcomeau.com/wham/02-svg/04.02-animation-exercises
---
## Blinking Budget Emoji

眨眼的練習。我只想到用 scaleY 的方式，這導致整個眼睛橢圓形都在動。
解答用的是： `ry`。

之前的課程中有講到，但是我沒有太過意識到 ([[Strokes and Fills]])。SVG 裡面的 presentational attributes 基本上就是 CSS properties。

https://courses.joshwcomeau.com/wham/02-svg/04-animated-svgs
文中也有提到並且示範：
Most single-value attributes, like `x` on a `<rect>` or `ry` on an `<ellipse>`, work great



## Hamburger / X

踩了個大雷。
```js
animate(line1, {
    x2:5,
    y2:16,
    x1:19,
    y1:16
});
```
x1 等屬性，不能給 string ，要給數字。
神奇的是給 string 會錯一半，沒有動畫效果，但是仍能變形。


## Play / Stop