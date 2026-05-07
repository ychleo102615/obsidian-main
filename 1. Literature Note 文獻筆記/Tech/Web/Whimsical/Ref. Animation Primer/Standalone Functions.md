---
tags: []
date: 2026-05-07
time: 15:03
---
```css
<style>
  @keyframes breathe {
    from {
      scale: 0.8;
    }
    to {
      scale: 1.2;
    }
  }
  @keyframes spin {
    from {
      rotate: 0deg;
    }
    to {
      rotate: 360deg;
    }
  }
  
  .elem {
    animation:
      breathe 1000ms ease-in-out infinite alternate,
      spin 12345ms linear infinite;
  }
</style>
```

##### breathe, spin 彼此互不影響

```css
<style>
  @keyframes breathe {
    from {
      transform: scale(0.8);
    }
    to {
      transform: scale(1.2);
    }
  }
  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }
  
  .elem {
    animation:
      breathe 1000ms ease-in-out infinite alternate,
      spin 12345ms linear infinite;
  }
</style>
```

##### breathe, spin 覆蓋 transform 屬性，所以只有 spin 生效。