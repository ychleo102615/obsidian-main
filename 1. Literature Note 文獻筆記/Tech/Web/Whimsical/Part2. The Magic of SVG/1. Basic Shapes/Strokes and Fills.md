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