---
tags: []
date: 2026-05-08
time: 14:03
link: https://courses.joshwcomeau.com/wham/01-particles/04.01-alternative-approach
---
```css
.particle {
	inset: 0px; /* short hand for top, left, bottom, right all set to same value. */
	margin: auto;
}

@keyframes fromCenter {
	from {
		/* 用程式碼(inline)設置終點的位置，但是用 from 設置初始位置 */
		transform: translate(0px, 0px);
	}
}
```



置中技巧
[How To Center a Div](https://www.joshwcomeau.com/css/center-a-div/#centering-with-auto-margins)

[[2026-06-23|2026-06-23 火, 10:36]]
我在想每次我遇到 -tranlate 50% 時，我都不喜歡這種做法，但是我又會突然想不起課程哪一篇有提到可以迴避這種用法的技巧。就是這篇，並且與置中技巧有關係。

