---
tags: []
date: 2026-05-29
time: 16:03
---

```css
.item {
    /* Tag all 16 words with the same View Transition class: */
    view-transition-class: connections-item;
}
/* ...and then apply the same animation settings to them all: */
::view-transition-group(.connections-item) {
    animation-duration: 500ms;
}
```

即使有 class ，還是需要 `view-transition-name` 作為瀏覽器辨別每一個元素的依據。
所以此時可以使用 
```css
view-transition-name: match-element;
```
