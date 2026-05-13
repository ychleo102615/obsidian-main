---
tags: []
date: 2026-05-13
time: 21:39
---

> [!NOTE]
> ##### Think of SVG as an alternative version of HTML that is focused on illustration rather than documentation.

```html
<circle>

<polygon>

<rect>

```


# Lines
```css
<svg width="280" height="280">
	<line
		x1="70"
		y1="110"
		x2="130"
		y2="160"
		stroke="oklch(0.9 0.3 164)"
		stroke-width="5"
	/>
</svg>
```

- 聲明兩個點的位置 (geometry attributes)
- 聲明顏色和粗度（presentational attributes）


# Rectangles
```css
<svg width="300" height="300">
	<rect
		x="60"
		y="100"
		width="180"
		height="100"
		fill="none"
		stroke="oklch(0.9 0.3 164)"
		stroke-width="5"
	/>
</svg>
```