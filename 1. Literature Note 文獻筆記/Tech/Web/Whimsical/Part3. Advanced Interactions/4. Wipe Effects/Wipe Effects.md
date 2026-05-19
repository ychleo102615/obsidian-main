---
tags: []
date: 2026-05-19
time: 17:21
---
## `clip-path` property

```html
<style>
  .box {
    width: 200px;
    height: 200px;
    background: linear-gradient(
      to top,
      red,
      yellow
    );
    clip-path: polygon(
      50% 0%,
      100% 50%,
      50% 100%,
      0% 50%
    );
  }
</style>

<div class="box"></div>
```


### Each value represents the distance from the origin point in the top-left corner.




## Intangible pixels
用 clip path 把圖示隱藏時，他同時也把 hover event 隱藏了