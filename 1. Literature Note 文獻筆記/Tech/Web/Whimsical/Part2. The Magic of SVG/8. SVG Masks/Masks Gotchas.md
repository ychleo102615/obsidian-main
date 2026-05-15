---
tags: []
date: 2026-05-15
time: 17:44
---

## Masks and transforms

我們不太能夠使用 CSS 操作複合的數值：
```html
<polygon
    mask="url(#triangle-mask)"
    points="
        19,20
        9,12
        19,4
    "
/>
```

我們可以直接移動 polygon 本身的 transform，但是他身上的 mask 也會一起移動，這可能不是我們想要的。

解法是把 mask 移到外層的 `<g>` tag
```html
<g mask="url(#triangle-mask)">
    <polygon
        points="
        19,20
        9,12
        19,4
      "
    />
</g>
```