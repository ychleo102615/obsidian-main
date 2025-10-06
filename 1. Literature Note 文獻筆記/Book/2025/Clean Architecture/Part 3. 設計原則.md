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


## 症狀1： 意外重複

```
Employee
calculatePay()   方法由會計部指定，向CFO報告
reportHours()    方法由人力資源部指定，向COO報告
save()           方法由資料庫管理員指定，向CTO報告
```

這個耦合可能會導致CFO團隊的行為影響了COO團隊所依賴的東西。
例如：calculatePay, reportHours共用了計算非加班時間的演算法，叫他regularHours()

CFO團隊決定非加班時間的計算方式需要調整，但是COO不想要。

==**分開不同角色所依賴的程式碼。**==


```mermaid
graph TD
    calculatePay["calculatePay"] --> regularHours["regularHours"]
    reportHours["reportHours"] --> regularHours

```

## 症狀2： 合併

不同團隊對`Employee`類別修改、碰撞，最終合併。
沒有工具可以處理每一個合併案裡，最後總是會有風險。

多人因不同原因而修改相同的原始檔。

**==分離支援不同角色的程式碼。==**

## 解決方案

一個明顯方法是將資料與函式分開。這三個類別共用了`EmployData`，這是一個沒有方法的簡單資料結構。
三個類別不允許了解彼此。因此避免了意外重複。

為了避免時力化和追蹤三個類別，使用`Facade`模式。

```mermaid
classDiagram
    class EmployeeFacade {
        +calculatePay()
        +reportHours()
        +save()
    }

    class PayCalculator {
        +calculatePay()
    }

    class HourReporter {
        +reportHours()
    }

    class EmployeeSaver {
        +saveEmployee()
    }

    class EmployeeData

    EmployeeFacade --> PayCalculator
    EmployeeFacade --> HourReporter
    EmployeeFacade --> EmployeeSaver

    PayCalculator --> EmployeeData
    HourReporter --> EmployeeData
    EmployeeSaver --> EmployeeData

```

每個類別都是一個視野範圍。在這個視野範圍之外，沒有人知道存在這個家族的私有成員。

# Ch8. OCP 開放封閉原則

**Open-Closed Principle**

軟體應該對於擴展開放，對於修改封閉。
Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.

架構師根據如何、為什麼級何時發生變更來分離功能，組織元件階層。
高層級元件受到保護，免受低層級元件的變更所影響。

## 總結
OCP是糸統架構背後的推動力之一。目標是使系統易於擴展而不會因修改產生較大的影響。
這個目標是透過將系統劃分為元件，並將這些元件安排到依賴階層中而實現的。
這種階層結構能保護較高層級的元件免受掉低層級元件的變更所影響。


> [!NOTE] 回顧心得
> 我覺得我當初第一次看一定是看不懂的。因為我現在是全部都懂了之後，再來看書上的那張圖，才非常有看懂的感覺。
> 他這張圖初見太複雜了。
> 
> ```mermaid
> graph LR
>     view["view"] --> presenter["presenter"] --> controlloer["controller"] --> interactor["interactor"]
>      database["database"] --> interactor["interactor"]
> ```


# Ch9. LSP Liskov 替換原則

## 指導繼承的使用
```mermaid
classDiagram
    class Billing {
        +calcFee()
    }
    class License {
        <<abstract>>
        +calcFee()
    }
    class PersonalLicense {
    }
    class BusinessLicense {
        -users
    }

    Billing --> License : uses
    License <|-- PersonalLicense : extends
    License <|-- BusinessLicense : extends
```

Billing的行為不以任何方式依賴於他使用的兩個子型態中的哪一個。這兩個子型態都可以替換License型態。

## 正方形／矩形問題

違反



