---
tags: []
date: 2026-05-15
time: 15:56
---

設定可視的部分
<svg viewBox="0 0 32 32">
  <defs>
    <mask id="moon">
      <rect x="0" y="0" width="32" height="32" fill="white" />
      <circle class="cutout" cx="24" cy="8" r="12" />
    </mask>
  </defs>
  
  <circle
    cx="16"
    cy="16"
    r="12"
    fill="hotpink"
    mask="url(#moon)"
  />
</svg>

很有趣的地方是，mask 本身也可以像是再被 mask 一次。
這個範例中聲明了：
- 白色全覆蓋的正方形
- 黑色圓形

黑色圓形的用途就像是在 mask 白色正方形。
而 mask 起作用的部分正是白色的部分，所以達到了這種嵌套效果。