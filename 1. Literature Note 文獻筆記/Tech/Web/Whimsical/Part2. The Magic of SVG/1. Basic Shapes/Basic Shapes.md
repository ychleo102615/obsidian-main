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

- 聲明左上角的點
- 聲明寬高
- 聲明線條顏色、粗度

stroke 必定從線的中央出發，無法調整（inside or outside）。


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
		/* optional */
		rx="100"
		ry="50"
		fill="none"
	/>
</svg>
```

- 圓角半徑。可以省略 ry 以表與 rx 相同
- 填滿效果


# Circles
```css
<svg width="280" height="280">
	<circle
		cx="140"
		cy="140"
		r="70"
		fill="none"
		stroke="oklch(0.9 0.3 164)"
		stroke-width="5"
	/>
</svg>
```

- 圓心、半徑
- 線條
- 填滿效果


# Ellipses
```css
<svg width="300" height="300">
	<ellipse
		cx="150"
		cy="150"
		rx="75"
		ry="50"
		fill="none"
		stroke="oklch(0.9 0.3 164)"
		stroke-width="5"
	/>
</svg>
```

- 半徑變成 rx, ry

# Polylines
```css
<svg width="280" height="280">
	<polyline
		points="
			60,100
			100,180
			140,140
			180,180
			220,100
		"
		fill="none"
		stroke="oklch(0.9 0.3 164)"
		stroke-width="5"
	/>
</svg>
```

他不是單純多個 line 而已>
