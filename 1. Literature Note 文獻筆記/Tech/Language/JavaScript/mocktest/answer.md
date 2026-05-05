---
tags: []
date: 2026-05-05
time: 16:21
---

1. [ ] A
2. [ ] B
3. [ ] A
4. [ ] A -
5. [x] A
6. [ ] B
7. [x] A-
8. [ ] D
9. [ ] B-
10. [ ] A
11. [ ] B-
12. [ ] B
13. [ ] A-
14. [ ] C
15. [ ] A-
16. [ ] A
17. [ ] A
18. [ ] B-
19. [ ] B
20. [x] D-
21. [ ] B
22. [ ] B
23. [ ] B-
24. [x] B
25. [ ] D
26. [x] D
27. [ ] B
28. [ ] A-
29. [ ] B - 題目敘述有問題
30. [ ] C
31. [x] A-
32. [ ] A-
33. [ ] C
34. [ ] A
35. [ ] A-
36. [ ] -
37. [ ] B
38. [ ] B
39. [ ] A
40. [ ] B
41. [x] B-
42. [ ] B

錯 7 題
不確定 14 題

##### Q4
Object.create 也會建立 `__proto__` 指向 Constructor.prototype

##### Q5
`Object.defineProperty`
三個參數：
- **obj**：目標物件。
- **prop**：要定義或修改的屬性名稱（字串或 Symbol）。
- **descriptor**：屬性描述符，用來設定該屬性的「特權」。

| 特徵           | 說明                               | 預設值       |
| ------------ | -------------------------------- | --------- |
| value        | 實際數值                             | undefined |
| writable     | 可否被 assign                       | false     |
| enumerable   | 是否出現在 for ... in 或 Object.keys() | false     |
| configurable | 可否刪除                             | false     |

用於 Vue2

##### Q7

default parameter 只有在 undefined 時才會生效，null 不會。
所以 `1 + null + 3` 會得到 `1 + 0 + 3 === 4`
另外，`1 + undefined + 3` 會得到 NaN。

##### Q11
switch 使用 `===` 比對。

##### Q13
`{} + []`
結果：`0` (在瀏覽器控制台中) 或 `"[object Object]"` (在某些環境或變數賦值時)

因為題目有這個前提：
(Assume each line is evaluated as an expression, not interpreted at statement level where `{}` could be parsed as a block.)
{} 不會被解析為 block ，所以答案不是 0。