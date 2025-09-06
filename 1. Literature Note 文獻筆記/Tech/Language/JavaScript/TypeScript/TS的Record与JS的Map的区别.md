---
tags: []
date: 2024-08-13
time: 11:41
---
[ref](https://blog.csdn.net/dongnihao/article/details/128444552)


## 简单理解：Record就是强类型的Map


record 有 3 大特色 
1. immutable 函数式提倡的东西. 对象创建后, 属性值就不可以修改了. var dimension = new Dimension(Width: 100, Height: 200); dimension.Width = 5; // Error: record 是 immutable 上面这样是直接 complie error 的. 
2. Deconstruct 类似 JavaScript 的解构, 它利用 Tuple 解构的特性. 
3. assign and clone immutable 要怎样修改 value 呢? 靠的是 clone 一个新的来赋值. var dimension = new Dimension(Width: 100, Height: 200); var newDimension = dimension with { Height = 100 }; 


When to use? 如果你有喜欢 immutable 和 with 这类特性, 那么就可以考虑用 record. 所以建议在DDD中，对于值对象，一般定义为Record类型。