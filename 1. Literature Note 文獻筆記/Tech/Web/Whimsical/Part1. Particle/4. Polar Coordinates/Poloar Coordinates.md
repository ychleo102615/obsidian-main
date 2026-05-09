---
tags: []
date: 2026-05-09
time: 20:57
---

### Cartesian Coordinates 笛卡兒

```css
@keyframes disperse {
	from {
		transform: translate(
			calc(cos(var(--angle)) * var(--distance)),
			calc(sin(var(--angle)) * var(--distance))
		);
	}
}
```

但讓 CSS 保持 Cartesian 會比較好，比較不複雜。