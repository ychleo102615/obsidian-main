---
tags: []
date: 2026-06-03
time: 13:37
---

 [Easings.net](https://easings.net/)

```js
// Timing functions!
// Find many more at https://easings.net
function easeInSine(x) {
  return 1 - Math.cos((x * Math.PI) / 2);
}
function easeOutSine(x) {
  return Math.sin((x * Math.PI) / 2);
}
function easeInOutSine(x) {
  return -(Math.cos(Math.PI * x) - 1) / 2;
}
function easeOutQuad(x) {
  return 1 - (1 - x) * (1 - x);
}
function easeOutExpo(x) {
  return x === 1 ? 1 : 1 - Math.pow(2, -10 * x);
}
function easeOutCirc(x) {
  return Math.sqrt(1 - Math.pow(x - 1, 2));
}
function easeOutBounce(x) {
  const n1 = 7.5625;
  const d1 = 2.75;

  if (x < 1 / d1) {
    return n1 * x * x;
  } else if (x < 2 / d1) {
    return n1 * (x -= 1.5 / d1) * x + 0.75;
  } else if (x < 2.5 / d1) {
    return n1 * (x -= 2.25 / d1) * x + 0.9375;
  } else {
    return n1 * (x -= 2.625 / d1) * x + 0.984375;
  }
}
```