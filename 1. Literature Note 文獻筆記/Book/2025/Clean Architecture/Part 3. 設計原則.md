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
calculatePay()   方法由會計部指定，向CFO報告
reportHours()    方法由人力資源部指定，向COO報告
save()           方法由資料庫管理員指定，向CTO報告
```

這個耦合可能會導致CFO團隊的行為影響了COO團隊所依賴的東西。
例如：calculatePay, reportHours共用了計算非加班時間的演算法，叫他regularHours()

CFO團隊決定非加班時間的計算方式需要調整，但是COO不想要。

我們需要分開不同角色所依賴的程式嗎。


```mermaid
graph TD
    calculatePay["calculatePay"] --> regularHours["regularHours"]
    reportHours["reportHours"] --> regularHours

```
