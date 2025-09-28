---
tags: []
date: 2025-09-28
time: 22:45
---

# SOLID 原則

- 能容忍變化
- 容易理解
- 元件的基礎

相關閱讀材料
- Agile Software Development, Principles, Patterns, and Practices
- Agile Principles, Patterns, and Practices in C#

# Ch7. SRP 單一職責原則

**Single Responsibility Principle**

#### 不是：每個模組應做一件事
#### 是：一個模組應該只有一個，且只有一個理由會使其改變

改變是為了滿足使用者和利益相關者，所以我們也可以說：
##### **一個模組應該只對唯一的一個使用者或利益相關者負責。**

再把需要這些變更的人稱為角色 actor 參與者

**一個模組應該只對唯一的一個角色負責。**

### 模組的定義
一個原始檔，或是一個由函式和資料結構相互凝聚（cohensive）在一起的集合。


## 症狀1. 意外重複

```
Employee
```