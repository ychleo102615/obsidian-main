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

以上的用法不允許重複點擊（上一次音效還在播放時，就無法觸發下次播放）