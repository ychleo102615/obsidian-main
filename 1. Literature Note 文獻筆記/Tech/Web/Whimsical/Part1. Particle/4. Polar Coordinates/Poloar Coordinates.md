---
tags: []
date: 2026-05-09
time: 20:57
link: https://courses.joshwcomeau.com/wham/01-particles/07-polar-coordinates
---

### Cartesian Coordinates 笛卡兒坐標系
就是直角坐標系（Rectangular Coordinates）

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

```js
const convertPolarToCartesian = (angle, distance) => {
	const angleInRadians = convertDegreesToRadians(angle);
	const x = Math.cos(angleInRadians) * distance;
	const y = Math.sin(angleInRadians) * distance;
	return [x, y];
};

const convertDegreesToRadians = (angle) => (angle * Math.PI) / 180;
```