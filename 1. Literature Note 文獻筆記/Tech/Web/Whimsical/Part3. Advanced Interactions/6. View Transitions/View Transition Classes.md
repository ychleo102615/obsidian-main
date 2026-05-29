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