---
tags: []
date: 2026-05-20
time: 00:39
---

## Staggered words

```css
animation-range: cover var(--start) cover var(--end); 
animation: var(--duration) var(--easing);
```
前者用法有問題，但是後者可以


```css
.word:nth-of-type(1) {
}

.word {
    animation-range:
        cover calc(20% + sibling-index() * 5%)
        cover calc(45% + sibling-index() * 5%);
}
@supports () {
}
```