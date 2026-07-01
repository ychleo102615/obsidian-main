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

我突然想到，我一直都很納悶，為什麼這裡用的是 extends？我今天在寫題目的時候，意外得直覺上可以懂怎麼用，但是仔細想想發現自己並不完全懂。

明明傳進去的可以是 `'GET'` 這樣的參數，為什麼會說他 extends `Method`呢？

我知道 `Dog extends Aninmal`，也覺得從物理層面上，我應該是要把東西加大。但是這邊怎麼反而是給一個更限縮、更像是子集合的東西呢（`GET`）？

從結論來說，我對 extends 的理解是「成員、物理」層面上的。但這裡的 extends 描述的是「條件上的擴充」。當「條件」被擴充了，「實例集合(合法值集合)」就變小了。

從「條件規則的擴充」這個角度來理解就能說得通了。

「實例集合(合法值集合)」變小，代表這是一個子集合。
- `'GET' extends Method `
- `Dog extends Animal`

所以就能夠理解為：**子集合 ⊆ 父集合** 、**子類別 ⊆ 父類別** 。

因為此時我們描述的是「**實例集合(合法值集合)**」
