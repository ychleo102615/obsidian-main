---
tags: []
date: 2026-05-15
time: 15:56
---

設定可視的部分

```css
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
```

很有趣的地方是，mask 本身也可以像是再被 mask 一次。
這個範例中聲明了