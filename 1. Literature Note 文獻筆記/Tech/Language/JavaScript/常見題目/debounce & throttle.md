---
tags: []
date: 2026-01-26
time: 22:52
---

```js
function debounce(fn, delay) {
	let timer = null
	return function(...args) {
		clearTimeout(timer)
		timer = setTimeout(function(){
			fn.apply(this)
		})
	}
}
```