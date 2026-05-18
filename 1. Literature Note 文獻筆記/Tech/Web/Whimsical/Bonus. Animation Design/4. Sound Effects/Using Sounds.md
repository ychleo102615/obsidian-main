---
tags: []
date: 2026-05-18
time: 16:34
---

```js
const btn = document.querySelector('button');

const audioElem = new Audio('/sounds/tink.mp3');

btn.addEventListener('click', () => {
  audioElem.play();
});

// 🙅 Bad idea:
btn.addEventListener('click', () => {
    const audioElem = new Audio('/sounds/tink.mp3');
    audioElem.play();
});
```