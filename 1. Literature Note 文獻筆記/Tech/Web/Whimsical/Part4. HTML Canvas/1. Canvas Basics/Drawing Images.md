---
tags: []
date: 2026-05-30
time: 15:22
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