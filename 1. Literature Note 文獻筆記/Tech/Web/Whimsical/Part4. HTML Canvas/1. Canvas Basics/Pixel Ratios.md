---
tags: []
date: 2026-05-30
time: 14:51
---
`window.devicePixelRatio`  這個數字代表的是，通常 css 中的 pixel 並不是真的對應上顯示器上面使用的 pixel 。我們可能會用更高解析度的顯示器 pixel 來顯示較低的 css pixel 。這麼做的壞處是在 canvas 上會顯得低解析度。

所以要用把實際的寬高設定的大一點。


```js
const canvas = document.querySelector('canvas');
const { ctx } = setupCanvas(canvas);

ctx.lineWidth = '4';
ctx.lineCap = 'round';
ctx.lineJoin = 'round';

ctx.beginPath();
ctx.moveTo(40, 120);
ctx.lineTo(80, 160);
ctx.lineTo(160, 40);
ctx.strokeStyle = 'green';
ctx.stroke();



function setupCanvas(canvas) {
  const ctx = canvas.getContext('2d');

  const { width, height } =
    canvas.getBoundingClientRect();

  const dpr = window.devicePixelRatio;

  canvas.setAttribute('width', width * dpr);
  canvas.setAttribute('height', height * dpr);

  ctx.scale(dpr, dpr);

  return {
    ctx,
    canvasWidth: width,
    canvasHeight: height,
  };
}
```


```css
image-rendering: pixelated;
```
防止 smoothing。