---
tags: []
date: 2024-12-13
time: 16:13
---
為什麼線性轉換的順序是由右至左？
我比較能接受的觀點是：
###  **數學規範與一致性**

- 矩陣乘法的定義與數學中線性變換的函數組合密切相關，而函數組合本身是從內到外（即右到左）執行的。  
    例如：f(g(h(x)))f(g(h(x)))，對應的矩陣組合是 H⋅G⋅F⋅xH⋅G⋅F⋅x，而不是反過來。
- 如果改成由左至右，就違背了這種數學語義，且可能造成在現有理論框架下的混亂。數學界對這種改變一般持謹慎態度，因為它可能會破壞現有知識體系的完整性。

在CCScale9Sprite中有一部分的功能在描述要先rotate，再translate。
互叫的順序是反過來的：
```
x' = TRx
```

```lua
t = CCAffineTransformTranslate(t, rect.origin.x + rect.size.height, rect.origin.y);
t = CCAffineTransformRotate(t, 1.57079633); -- 90 degrees
...
-- 上面的線性轉換與下面的rect轉換、concat，參數順序是反過來
rect = CCRectApplyAffineTransform(rect, t);

-- t = CCAffineTransformConcat(CCAffineTransformMake(0, 1, -1, 0, 0, 0), t); -- 90 degrees
```

`CCRectApplyAffineTransform(rect, t), CCPointApplyAffineTransform(point, t), CCAffineTransformConcat(t1, t2)`這幾個函式的概念，都是由左至右的算法。
```
            |a  b  0|
[x, y, 1] x |c  d  0|
			|tx ty 1|

```

