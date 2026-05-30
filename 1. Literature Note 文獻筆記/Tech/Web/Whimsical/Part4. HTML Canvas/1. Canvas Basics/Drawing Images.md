---
tags: []
date: 2026-05-30
time: 15:22
link: https://courses.joshwcomeau.com/wham/04-canvas/01.04-loading-images
---

```js
const ctx = canvas.getContext('2d');
// Create an <img> element:
const img = new Image();
img.addEventListener("load", () => {
    // When the image has finished loading, draw it onto the canvas:
    const x = 0;
    const y = 0;
    ctx.drawImage(img, x, y);
});
// Set the `src` attribute to begin loading the image:
img.src = "/images/some-image.png";
```


Image 物件本質上就一個 `<img>` 元素。

Image 物件的 src 也可以來自 url, base64, svg。