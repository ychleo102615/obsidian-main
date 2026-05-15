---
tags: []
date: 2026-05-15
time: 22:13
---

`useId()` hook
可以避免我們的 id 重複。

另外比起使用 `crypto.randomUUID()`，`useId` 在 SSR 的情況下， client, server 仍能產生一樣的 id 。