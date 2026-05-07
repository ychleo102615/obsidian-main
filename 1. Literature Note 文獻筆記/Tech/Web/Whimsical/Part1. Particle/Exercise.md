---
tags: []
date: 2026-05-07
time: 18:10
---
```css
.startLayer {
	inset: 0;
	position: absolute;
	/*常用於遮罩*/
	overflow: hidden;
	user-select: none;
	pointer-events: none; /* 問 Claude 時，他給我 */
}

.particle::selection {
	/* pointer events 替代 */
	background: transparent;
}
```