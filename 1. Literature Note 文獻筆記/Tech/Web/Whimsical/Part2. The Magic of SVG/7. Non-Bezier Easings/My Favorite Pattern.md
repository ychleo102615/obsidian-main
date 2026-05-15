---
tags: []
date: 2026-05-15
time: 13:34
---



## Storing durations
```css
html {
    --spring-smooth: linear(...);
    --spring-smooth-time: 1000ms;
    --spring-bounce: linear(...);
    --spring-bounce-time: 1200ms;
    --spring-snappy: linear(...);
    --spring-snappy-time: 100ms;
}
.elem {
    transition:
    transform var(--spring-bounce) var(--spring-bounce-time);
}
```

把 duration 也一起存下來。