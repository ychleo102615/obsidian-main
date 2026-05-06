---
tags: []
date: 2026-05-06
time: 17:08
---
實際考完有不確定的地方：

- arguments 是 function 預設的變數沒錯
- `export {__ as __}` 有這種用法
- `substr(start, length)` 有這種用法，但是少用

```javascript
{
	start: 1,
	end: 3,
	[Symbol.iterator]() {
		let cur = this.start;
		let end = this.end;
		return {
			next() {
				...
			}
		};
	}
}
```