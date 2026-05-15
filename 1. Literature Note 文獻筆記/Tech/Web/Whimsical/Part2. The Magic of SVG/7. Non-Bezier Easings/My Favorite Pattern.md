---
tags: []
date: 2026-05-15
time: 13:34
---

## The simplest approach
常用的 timing function 存成全域 CSS 變數。

```css
html {
    --color-primary: hsl(...);
    --color-secondary: hsl(...);
    --spring-smooth: linear(...);
    --spring-bounce: linear(...);
    --spring-snappy: linear(...);
}
/* And then, we use it like this: */
.elem {
    transition: transform var(--spring-bounce) 1200ms;
}
```

這種全域變數的利用率，最好要有 80%。

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



## Fallbacks for older browsers

```css
.elem {
    /* fallback for older browsers: */
    color: hsl(340deg 100% 55%);
    /* modern version: */
    color: oklch(0.66 0.3 11.52);
}
```

上述的 fallback 用法不適用 CSS variable。

```css
html {
    --spring-smooth: cubic-bezier(...);
    --spring-smooth-time: 1000ms;
    @supports (animation-timing-function: linear(0, 1)) {
        --spring-smooth: linear(/* Lots of values here */);
    }
}
```

舊的瀏覽器不支援 `linear()`