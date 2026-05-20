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


|選擇器|類型|意義|
|---|---|---|
|`::view-transition-group(*)`|偽元素|View Transition API 建立的虛擬過渡群組節點|
|`:root`|偽類|文件根元素（`<html>`）的「根身份」狀態|
偽類的定義是：**不基於 HTML 標籤名稱，而是基於其他條件來選取元素**。