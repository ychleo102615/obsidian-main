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

##### The `prefers-reduced-motion` media query only has two possible values:
`reduce`: true
`no-preference`: false


### Accessing motion preferences in JavaScript

```js
function checkMotionPreferences() {
  const isMotionEnabled = window.matchMedia(
    '(prefers-reduced-motion: no-preference)'
  ).matches;
  return isMotionEnabled;
}

console.log(checkMotionPreferences()); // `true` or `false`
```

##### 為什麼不檢查 reduced 而是 no-preference？
瀏覽器可能沒有支持 prefers-reduced-motion，所以用 checkEnabled 的方式更保守。

##### React 中免去不同步的問題的方式：usePrefersReducedMotion
https://www.joshwcomeau.com/snippets/react-hooks/use-prefers-reduced-motion/


# template


```css
@media (prefers-reduced-motion: reduce) {

}
```
```css
@media (prefers-reduced-motion: no-preference) {

}
```