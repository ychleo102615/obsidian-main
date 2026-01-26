---
tags: []
date: 2026-01-26
time: 22:52
---

```js
function debounce(fn, delay) {
	let timer = null
	return function(...args) {
		// null 也不會報錯
		clearTimeout(timer)
		timer = setTimeout(function(){
			timer = null
			fn.apply(this, args)
		}, delay)
	}
}
```


```js
function throttle(fn, interval) {
	let lastTime = null
	return function(...args) {
		if (lastTime && new Date() - lastTime < interval) {
			return
		}
		fn.apply(this, args)
	}
}
```