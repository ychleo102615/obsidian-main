---
tags: []
date: 2026-05-07
time: 18:10
---
```css
.startLayer {
	inset: 0;
	position: absolute;
	/*常用於遮罩*/
	overflow: hidden;
	user-select: none;
	pointer-events: none; /* 問 Claude 時，他給我 */
}

.particle::selection {
	/* pointer events 替代 */
	background: transparent;
}
```


# Shimmer Particle
```css
@keyframes moveRight {
    from {
      translate: -100%;
    }
    to {
      translate: 100%;
    }
  }
  .shimmer {
    position: absolute;
    inset: 0;
    height: 100%;
    width: 100%;
    background: linear-gradient(
      to right,
      transparent,
      hsl(180deg 100% 90%),
      transparent
    );
    opacity: 0.5;
    animation: moveRight forwards;
  }

```

課程中示範了另一種實作可能性：使用 transition。
```css
.shimmer {
	transform: translateX(-100%);
	transition: transform 1000ms;
}
.buyButton:hover .shimmer {
	transform: translateX(100%);
}
```
雖然程式碼簡單很多，但是這有個副作用，當滑鼠移開時他會像乒乓球一樣來回。