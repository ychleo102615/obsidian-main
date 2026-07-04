---
tags: []
date: 2026-07-04
time: 15:07
link: https://typehero.dev/challenge/parameters/solutions
---

```ts
type MyParameters<T extends (...args: any[]) => any> = T extends (...args: infer P) => any ? P : never;
```

T extends 寫兩次的原因是：他們是**兩個不同時機、不同目的的檢查**：第一個是防呆（fail fast，錯誤訊息對使用者更友善），第二個是型別邏輯運算的必要條件。官方寫法保留第一個是工程上的良好實踐，但拿掉它程式仍然能跑，只是失去了在呼叫端就報錯的效果。