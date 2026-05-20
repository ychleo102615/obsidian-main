---
tags: []
date: 2026-05-20
time: 12:33
---

```css
  main {
    timeline-scope: --content;
  }

  .content {
    outline: 1px solid;
    view-timeline: --content;
  }
  .square {
    animation: demo both;
    animation-timeline: --content;
    animation-range: contain;
  }
  
```

在共同祖先中聲明變數。