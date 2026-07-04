---
tags: []
date: 2026-07-04
time: 23:21
link: https://typehero.dev/challenge/concat
---

```ts
type Concat<T extends readonly any[], U extends readonly any[]> = [...T, ...U]
```

我很納悶為什麼以下會是正確的：
```ts
Expect<Equal<Concat<[], [1]>, [1]>>,
```

明明是普通的 array ，他卻 extends 