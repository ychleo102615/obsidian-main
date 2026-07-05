---
tags: []
date: 2026-07-05
time: 22:24
link: https://typehero.dev/challenge/tuple-to-object
---

題目：
```ts
const tuple = ['tesla', 'model 3', 'model X', 'model Y'] as const

type result = TupleToObject<typeof tuple> // expected { 'tesla': 'tesla', 'model 3': 'model 3', 'model X': 'model X', 'model Y': 'model Y'}
```

一個問題是：要怎麼把 array 轉成 union？

答案：
 **index into the array type using the `number` keyword**.
```ts
type ExpectedProperty = string | number | symbol 
type TupleToObject<T extends readonly ExpectedProperty[]> = {
    [K in T[number]]: K ;
}
```