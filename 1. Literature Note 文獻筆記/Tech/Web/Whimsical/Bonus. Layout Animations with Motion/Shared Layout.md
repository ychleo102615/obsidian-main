---
tags: []
date: 2026-06-04
time: 21:13
link: https://courses.joshwcomeau.com/wham/05-motion-and-react/04-layout-id
---

共用一個 div 來作為 hovered 的背景。這個單元中介紹切換時的動畫。
但我一直覺得沒有淡出淡入很怪。研究一下之後，要多加幾個步驟：

```jsx
<AnimatePresence>
  {hoveredNavItem === slug && (
    <motion.div
      layoutId="hovered-backdrop"
      className="hovered-backdrop"
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
      transition={{ duration: 0.3 }}
    />
  )}
</AnimatePresence>
```

1. 使用 initial, animate, exit
2. 使用 AnimatePresence 包住