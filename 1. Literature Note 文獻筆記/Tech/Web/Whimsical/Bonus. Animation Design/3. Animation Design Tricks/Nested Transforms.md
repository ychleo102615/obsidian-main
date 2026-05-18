---
tags: []
date: 2026-05-18
time: 14:38
---

```css
.fuse {
    transition: transform 400ms;
    transform-origin: 50% 100%;
  }
  .wrapper {
    transition: transform 400ms;

    &:hover {
      transform: rotate(45deg);

      .fuse {
        transform: rotate(135deg);
      }
    }
  }
```