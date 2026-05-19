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