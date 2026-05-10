---
tags: []
date: 2026-05-10
time: 21:59
link: https://courses.joshwcomeau.com/wham/01-particles/10-linear-interpolation
---

```js

// 這種程式碼沒有辦法一眼就看出用途
const angle = index * (360 / NUM_OF_PARTICLES);

// 講師認為這樣的寫法更直觀，這種用法他非常常用。
const angle = normalize(index, 0, NUM_OF_PARTICLES, 0, 360);

```


[工具函式集](https://courses.joshwcomeau.com/wham/01-particles/10.02-lerp-utils)
```js
export const clamp = (
	value,
	min = 0,
	max = 1
) => {
	if (min > max) {
		[min, max] = [max, min];
	}
	return Math.max(min, Math.min(max, value));
};

export const normalize = (
	value,
	currentScaleMin,
	currentScaleMax,
	newScaleMin = 0,
	newScaleMax = 1
) => {
	const standardNormalization = (value - currentScaleMin) / (currentScaleMax - currentScaleMin);
	return (
		(newScaleMax - newScaleMin) * standardNormalization + newScaleMin
	);
};

export const clampedNormalize = (
	value,
	currentScaleMin,
	currentScaleMax,
	newScaleMin = 0,
	newScaleMax = 1
) => {
	return clamp(
		normalize(
			value,
			currentScaleMin,
			currentScaleMax,
			newScaleMin,
			newScaleMax
		),
		newScaleMin,
		newScaleMax
	);
};

// In addition to _linear_ interpolation, I sometimes want to use _exponential_ interpolation, where the input is mapped onto a curved line rather than a straight one. This is beyond the scope of this lesson, but feel free to experiment with this!

export const exponentialNormalize = (
	value,
	currentScaleMin,
	currentScaleMax,
	newScaleMin = 0,
	newScaleMax = 1,
	exponent = 2
) => {
	const normalizedInput =
		(value - currentScaleMin) / (currentScaleMax - currentScaleMin);
	const exponentialOutput = Math.pow(normalizedInput, exponent);
	return (
		newScaleMin + (newScaleMax - newScaleMin) * exponentialOutput
	);
};
```