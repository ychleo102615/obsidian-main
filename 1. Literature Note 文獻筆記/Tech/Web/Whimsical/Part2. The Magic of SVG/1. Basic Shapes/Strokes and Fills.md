---
tags: []
date: 2026-05-13
time: 22:27
---
presentational attributes 其實就是 CSS


# Fills

想要用 SVG attribute 或是 CSS property 都可以。
但是講者也提到在 React, Vue 中 attribute 會更容易操作一點。

預設是黑色，想要避免這個行為的話可以設置為 `none`


### Inheriting text color

```html
<div style="color : red;">
    ...
    <circle
        fill="currentColor"
    />
    ...
</div>
```

### Fill opacity
`fill-opacity`

# Strokes

### Allowing overflow
```css
svg {
    overflow: visible;
}
```

### Stroke Opacity
`stroke-opacity`

### Caps and joins
邊緣連接處的處理

`stroke-linecap`: `butt | round | square`
`stroke-linejoin`: `miter | round | bevel`

### Dashes
`stroke-dasyarray` = "10, 10"
控制虛線。描述 dash, gap 的長度。

`stroke-dashoffset` 調整位置

文中示範了一種應用，與我的個人專案花牌的等待配對 loading 動畫很像：
```css
<svg width="276" height="276">
    <circle
        cx="138"
        cy="138"
        r="87.54"
        stroke-width="5"
        stroke-dasharray="100,450"
        stroke-dashoffset="480"
        stroke-linecap="round"
    />
</svg>
```

虛線的效果像是一個圈上只有一段有 stroke。調整 `stroke-dashoffset` 