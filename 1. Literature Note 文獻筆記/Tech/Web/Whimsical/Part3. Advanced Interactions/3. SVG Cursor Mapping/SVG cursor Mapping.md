---
tags: []
date: 2026-05-19
time: 15:28
---

操作 SVG 會遇到的問題：內外 scale 不一致。
SVG 本身就有內部的座標系統。


```js
const scaledX = normalize(relativeX, 0, bb.width, 0, VIEW_BOX_SIZE);
```


```js
  const point = svg.createSVGPoint();
  point.x = event.clientX;
  point.y = event.clientY;

  const { x, y } = point.matrixTransform(
    svg.getScreenCTM().inverse()
  );

  circle.setAttribute('cx', x);
  circle.setAttribute('cy', y);
```