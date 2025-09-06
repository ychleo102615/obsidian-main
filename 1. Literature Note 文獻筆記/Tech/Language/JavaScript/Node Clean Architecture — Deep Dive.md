---
tags: []
date: 2024-07-10
time: 16:39
---
[Node Clean Architecture — Deep Dive](https://betterprogramming.pub/node-clean-architecture-deep-dive-ab68e523554b)

同時參考：
[[4. 無暇的程式碼—整潔的軟體設計與架構篇]]
[[5. Clean Architecture 實作篇：在整潔的架構上弄髒你的手]]

在逛nestjs如何寫的時候，逛到了這篇文章。他用node來實踐clean code，比起**實作篇**這本書教的樣式，這個作者也提供了另外一種架構組裝版本。


```
作者範例

StudentController ----  AddStudent      ----- StudentRepository
						GetAllStudents        CrmServices
						GetStudent
						AddEnrollment
				
```

### Controller 抽象介面省略
controller對use case，依賴方向與控制流方向是一樣的。多用一個抽象介面確實是挺雞肋。就算是用Java寫應該也一樣，不需要多一個抽象介面。

### Use-case factory method
其中一個很不一樣的是：作者用工廠方法包裝了使用案例。一個使用案例的本質也就是一個函式而已。
等於是use case是動態組裝的，而不是在最初期建構期。

#### 所以，最開始的建構初期，其實只有組裝Controller而已。

