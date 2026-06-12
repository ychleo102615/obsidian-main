---
tags: []
date: 2026-05-19
time: 15:28
link: https://courses.joshwcomeau.com/wham/03-advanced-interactions/03-mapping-cursor-to-svg
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

  `SVGMatrix { a: 1.565, b: 0, c: 0, d: 1.565, e: 78.25, f: 276.25 }`
  
  CTM = Current Transformation Matrix

```js
const point = new DOMPoint(event.clientX, event.clientY); 
const { x, y } = point.matrixTransform(svg.getScreenCTM().inverse());
```

變換矩陣