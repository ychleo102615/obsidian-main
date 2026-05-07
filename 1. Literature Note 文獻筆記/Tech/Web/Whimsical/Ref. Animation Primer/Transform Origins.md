---
tags: []
date: 2026-05-07
time: 14:40
---

```css
transform-origin: center;
transform-origin: left top;
transform-origin: 25px bottom;
transform-origin: 0% 150%;
```


translate 時，origin 也不會動。所以先 translate 再 rotate，會造成 rotate 用很大的半徑在旋轉的效果。

使用 CSS 時，似乎不需要思考繪製的本質和線性代數。
CSS 會自動依照你寫的順序：
```css
transfomr: translateX(100px) rotate(90deg);
transfomr: rotate(100px) translateX(90deg);
```

下面那行來說，先旋轉 90 度再 translateX 的話，X 正的方向等同於 Y 的正向（本來往右，變成往下）。