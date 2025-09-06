---
tags: []
date: 2024-07-12
time: 11:38
---
- [ ] [DCI架构是如何解决DDD战术建模缺点的？](https://blog.csdn.net/maoyeqiu/article/details/121619519)
[領域驅動設計學習筆記（16）：學DCI，重構Aggregate ，Part 1](https://teddy-chen-tw.blogspot.com/2021/06/16dciaggregate-part-1.html)

# Data, Context, Interaction

在看到貧血模型與充血模型的比較分析時遇到的架構。他指出有時候充血模型可能會耦合太多功能在裡面，所以出了一個新架構。

指在不同的情境 Context （例如學校、工作）之下，一個模型可以有不同的資料與行為，可以被拆出為身份 Role（學生身份、員工身份）。

> [!cite] 
> Coplien認為唯有給定一個Context再去解讀物件身上的行為才會有意義，程式也比較容易被讀懂。

