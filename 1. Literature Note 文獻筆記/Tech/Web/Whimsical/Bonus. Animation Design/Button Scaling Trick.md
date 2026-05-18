---
tags: []
date: 2026-05-18
time: 11:39
---


按鈕放大是一個常見的 hover 特效。
但是放大的時候，會有一點糊掉。講者說這是 CPU 轉 GPU 繪製有關。

```css
  .btn {
    position: relative;
    border: none;
    background: transparent;
  }
  .btn::before {
    content: '';
    position: absolute;
    inset: 0;
    border: 1px solid hsl(210deg 15% 25%);
    border-radius: 4px;
    transition: transform 200ms;
  }
  .btn:hover::before {
    transform: scale(1.1);
  }
```

使用 pseudo-element 繪製邊框，這樣 parent button 的文字就不會受到影響。