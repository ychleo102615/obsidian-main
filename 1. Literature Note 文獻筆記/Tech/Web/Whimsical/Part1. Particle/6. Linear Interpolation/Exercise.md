---
tags: []
date: 2026-05-10
time: 22:38
link: https://courses.joshwcomeau.com/wham/01-particles/10.01-lerp-exercises
---

最後一個練習蠻有趣的。

作者的解答基本上提供了另外一種解題觀點。和本章先前提到的「為了提升可讀性而改寫」感覺很像。

```js
clamp(
	normalize(value, 0, 60, 0.01, 1),
	0.01,
	1
);
```