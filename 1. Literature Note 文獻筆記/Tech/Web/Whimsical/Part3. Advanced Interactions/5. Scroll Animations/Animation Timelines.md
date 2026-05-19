---
tags: []
date: 2026-05-19
time: 21:35
---
```css
.box {
    animation: spin;
    animation-timeline: scroll();
    animation-timeline: view();
    animation-range: contain;
    animation-range: cover;
    animation-range: entery 0% entry 150%;
}
```

```css
.box {
    animation: fadeIn linear both;
    animation-timeline: view();
    /* This line: */
    animation-range: entry 0% entry 150%;
    /* ...is a shorthand for: */
    animation-range-start: entry 0%;
    animation-range-end: entry 150%;
}
```