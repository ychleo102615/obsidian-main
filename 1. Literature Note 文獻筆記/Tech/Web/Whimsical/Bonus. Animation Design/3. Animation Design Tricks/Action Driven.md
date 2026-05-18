---
tags: []
date: 2026-05-18
time: 14:18
---

以動畫本身來驅動。
文中以 "open", "confirm", "cancel" 作為主要描述分類。

```css
.dialog {
    /* Hidden by default */
    transform: translateY(100%);
    
    &[data-action="open"] {
      transform: translateY(0);
      transition: transform 300ms;
    }
    &[data-action="cancel"] {
      filter: blur(10px);
      transform: translateY(100%) rotate(-20deg);
      opacity: 0;
      transition:
        transform 500ms,
        opacity 500ms,
        filter 500ms;
    }
    &[data-action='confirm'] {
      transform: translateY(100%);
      transition:
        transform 600ms cubic-bezier(0.54, -0.8, 1, 0.9);
    }
```

一個有趣的情境是，使用者快速 cancel 又 open 的話會怎麼樣？