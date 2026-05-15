---
tags: []
date: 2026-05-15
time: 22:21
---

```html
<motion.path />

// 渲染後變這樣
<path />
```

這裡的範例來自 [[1. Literature Note 文獻筆記/Tech/Web/Whimsical/Part2. The Magic of SVG/4. SVG Animations/Exercise|4. SVG Animations/Exercise]]

原本的做法要監聽 handleClick 的事件，手動呼叫：
```js
const path = button.querySelector('path');
animate(path, {
    d: 
        d: 'M 5,3\
        L 19,12\
        L 19,12\
        L 5,21\
        Z'
});
```


React 則是用聲明式的方式：
```jsx
<svg viewBox="0 0 24 24">
    <motion.path
        initial={false}
        animate={{
            d: isPlaying
              ? `
                M 4, 4
                L 20, 4
                L 20, 20
                L 4, 20
                Z
              `
              : `
                M 5, 3
                L 19, 12
                L 19, 12
                L 5, 21
                Z
              `,
        }}
    />
</svg>
```
