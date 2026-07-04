---
tags: []
date: 2026-07-04
time: 14:46
link: https://typehero.dev/challenge/pick/solutions/3764
---

TypeHero 上面的練習題


我的嘗試：
```ts
type MyPick<T, K> = {
    [Key in keyof T]: Key extends K ? T[Key] : never ;
};
```

解答：
```ts
type MyPick<T, K extends keyof T> = { 
    [P in K]: T[P];
};
```

我理解錯誤的地方：
1. 當塞入沒有在 T 裡面的 key 值時，我需要 `tx-expect-error`。所以 `K extends keyof T` 會是必要的。
2. 注意 K 已經是 union 了，所以有 `[P in K]` 這樣的用法。