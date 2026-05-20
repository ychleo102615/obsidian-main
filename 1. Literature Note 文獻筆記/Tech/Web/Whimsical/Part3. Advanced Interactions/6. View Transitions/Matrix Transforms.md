---
tags: []
date: 2026-05-20
time: 16:00
---

在跑 view transition 的時候，我們可以覆寫瀏覽器自動建立的 keyframe animations

```css
@keyframes changeOutline {
    from {
      outline: 10px solid blue;
    }
    to {
      outline: 1px solid yellow;
    }
  }
  
  ::view-transition-group(*) {
    animation-name: changeOutline; /* 使用自訂動畫 */
    animation-duration: 1000ms;
    border-radius: 6px;
  }
```