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

克ㄔ