---
tags: []
date: 2026-05-12
time: 12:38
link: https://courses.joshwcomeau.com/wham/01-particles/11-motion-accessibility
---

如果使用者在電腦上設定不想要有動態的話，可以用 @media 來知道這項偏好。
```css
.animated-button {
	animation: bounce 1000ms;
}

@media (prefers-reduced-motion: reduce) {
	.animated-button {
		animation: none;
	}
}
```

或者是在條件符合下才增設動畫：
```css
@media (prefers-reduced-motion: no-preference) {
	.animated-button {
		transition: transform 1000ms;
	}
}
```