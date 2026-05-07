---
tags: []
date: 2026-05-07
time: 21:12
link: https://courses.joshwcomeau.com/wham/01-particles/02-containment-strategies
---

# Anchor Point 問題
使用 left, top 對齊時，你會發現 `0%` `100%` 並不是貼著兩側邊緣。
`0%`在左側邊緣之內，而且不會碰到左側邊緣。
`100%`在右側邊緣之外，造成 overflow 。

一個簡單的解法是這樣：
```css
.star {
  position: absolute;
  transform: translate(-50%, -50%);
}
```

> [!NOTE] 百分比計算邏輯差異
> left, top 的百分比應用在 container 尺寸上。
> 但是 `transform: translate(-50%, -50%);` 這樣的寫法，計算會應用在元素自己身上 ([[Transforms]])。


# Perfect Containment
完全不 overflow 的配置方式。透過同時操作 left, transform translateX 來完成：
```css
  .star {
    /* Tweak these values to see the containment: */
    --top: 0%;
    --left: 100%;
    
    position: absolute;
    top: var(--top);
    left: var(--left);
    transform: translate(
      calc(var(--left) * -1),
      calc(var(--top) * -1)
    );
  }
```