
取得function回傳的type:
```ts
type T0 = ReturnType<() => string>;
// type T0 = string
```
 [參考](https://www.typescriptlang.org/docs/handbook/2/typeof-types.html)

取得type property 中的type
```ts
type Person = { age: number, name: string, alive: boolean };
type A = Person["age"];
// type A = number
```
[參考](https://microsoft.github.io/TypeScript-New-Handbook/chapters/types-from-extraction/)
