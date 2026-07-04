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

明明是普通的 array ，他卻 `extends readonly any[]`。

這個原因是 readonly 的 array 是缺少 push, pop 等方法的定義的，所以從 set 的角度來說，普通的 array 確實 extends readonly array。

---

補充：
規則一：`extends`（conditional type 判斷）不看 readonly
```ts
interface A { x: number }
interface B { readonly x: number }

type Test1 = A extends B ? true : false; // true
type Test2 = B extends A ? true : false; // true
```
規則二：賦值相容（assignability）會看 readonly，但方式不是「排除成員」
```ts
let a: { x: number } = { x: 1 };
let b: { readonly x: number } = { x: 1 };

a = b; // 編譯錯誤
b = a; // 合法
```

|機制|何時發生|readonly|union 分佈|excess property check|
|---|---|---|---|---|
|賦值檢查|賦值、傳參數、return|會檢查|無|有（限字面值）|
|conditional type extends|型別層級判斷|忽略|會分佈|無|
|interface extends|宣告當下|不適用|不適用|不適用|
