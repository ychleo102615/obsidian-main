---
tags: []
date: 2026-07-01
time: 23:45
---

簡單記錄一下想法。

我在做 [TypeHero](https://typehero.dev/challenge/default-generic-arguments) 的這條題目：

```ts
type Method = 'POST' | 'GET';
type ApiRequest<T, R extends Method = 'GET'> = {
    data: T,
    method: R
};
```

我突然想到，我一直都很納悶，為什麼這裡用的是 extends