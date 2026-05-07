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

使用 CSS 時，似乎不需要思考繪製的ㄅㄣ