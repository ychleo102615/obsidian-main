---
tags: []
date: 2026-01-07
time: 22:52
---


# == （抽象相等）

| **比較對象**                   | **轉換行為**                                       |
| -------------------------- | ---------------------------------------------- |
| **同型別** (String vs String) | **不轉型**，直接比較值（跟 `===` 一樣）。                     |
| **null vs undefined**      | **不轉型**，直接回傳 `true`。                           |
| **數字 vs 字串**               | 將 **字串** 轉為 **數字**。                            |
| **布林值 vs 其他**              | 將 **布林值** 轉為 **數字** (0 或 1)，再繼續比較。             |
| **物件 vs 原始值**              | 將 **物件** 轉為 **原始值** (透過 `toString`/`valueOf`)。 |

參考：轉型 [document](https://262.ecma-international.org/6.0/#sec-type-conversion)

### 一元運算子
```js
console.log(+'1');  // 1
console.log(+true);  // 1
console.log(+false);  // 0
```

### 邏輯運算子
```js
console.log(!0); // true
console.log(!1); // false

// 常用
console.log(!!1); // true
console.log(!!0); // false

```

### 二元運算子

#### + 運算子

前後運算子其一為字串或物件，則視為字串運算子。否則視為算數運算子。
```js
console.log(1 + '句子') // "1句子"
console.log(true + true) // 2
console.log(1 + {}) // "1[object Object]"
console.log(1 + [1]) // 11
console.log(1 + [1,2]) // 11,2
```

Number, BigInt 無法混合計算。