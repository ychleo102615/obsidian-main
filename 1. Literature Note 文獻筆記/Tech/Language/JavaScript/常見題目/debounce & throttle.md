---
tags: []
date: 2026-01-26
time: 22:52
---

```js
function debounce(fn, delay) {
	let timer = null
	return function(...args) {
		// null, 無效 id 也不會出錯
		clearTimeout(timer)
		timer = setTimeout(function(){
			// timer = null 
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
		lastTime = new Date()
	}
}

function throttle(fn, interval) {
	let lastTime = 0
	return function(...args) {
		const now = new Date()
		if (now - lastTime >= interval) {
			fn.apply(this, args)
			lastTime = now
		}
	}
}
```

Vue
```js
import { watchDebounced } from '@vueuse/core'

const keyword = ref('')

watchDebounced(
  keyword,
  (value) => {
    console.log('搜尋:', value)
  },
  { debounce: 300 }
)
```

```js
import { watchThrottled } from '@vueuse/core'

const scrollY = ref(0)

watchThrottled(
  scrollY,
  (value) => {
    console.log('位置:', value)
  },
  { throttle: 100 }
)
```
