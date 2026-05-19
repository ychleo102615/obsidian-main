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


- [View Timeline Range Visualizer (opens in new tab)](https://scroll-driven-animations.style/tools/view-timeline/ranges)
    
- [“Scroll-Driven Animations Debugger” Chrome extension](https://chromewebstore.google.com/detail/scroll-driven-animations/ojihehfngalmpghicjgbfdmloiifhoce)


想要 scroll 純粹按照最外層卷軸觸發時：
```css
.box {
    animation: spin linear;
    animation-timeline: scroll(root block);
}
```