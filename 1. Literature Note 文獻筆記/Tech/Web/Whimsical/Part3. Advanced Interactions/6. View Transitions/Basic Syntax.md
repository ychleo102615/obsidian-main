---
tags: []
date: 2026-05-20
time: 15:18
---

```css
  ::view-transition-group(*) {
    /* Increase me if you want to poke at the DOM: */
    animation-duration: 600ms;
  }
  ::view-transition-old(slideshow) {
    animation-name: exitLeft;
  }
  ::view-transition-new(slideshow) {
    animation-name: enterRight;
  }
  
  :root {
    view-transition-name: none;
  }
  .slideshow-img {
    view-transition-name: slideshow;
  }
  .next-btn {
    view-transition-name: next-btn;
  }
```