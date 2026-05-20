---
tags: []
date: 2026-05-20
time: 12:53
---

### 使用 IntersectionObersever

```js
const box = document.querySelector('.box');

const options = {
  threshold: 1,
  rootMargin: '32px',
  /* Required only because we’re running within an iframe: */
  root: document,
}

const observer = new IntersectionObserver((entries) => {
  const [entry] = entries;

  console.log(`Is intersecting: ${entry.isIntersecting}`);
  
  if (entry.isIntersecting) {
    box.classList.add('visible');
  } else {
    box.classList.remove('visible');
  }
}, options);

observer.observe(box);
```

### 手動間聽