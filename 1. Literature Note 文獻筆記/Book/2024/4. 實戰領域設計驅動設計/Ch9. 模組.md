---
tags: []
date: 2024-12-25
time: 23:57
---
模組在Java當中叫做套件（package），在C#中叫做命名空間（namespace）。Ruby則是採用與DDD設計模式同樣的名稱，以module關鍵字來達到建立類別命名空間的效果。

## 運用模組設計
模組在模型中的作用在於，將彼此之間具有高度內聚力的領域物件類別，以具名的容器打包在一起。不同模組的類別之間應該是低耦合的關係。

> [!NOTE] 領域驅動設計 p.109
> 選擇能夠描述系統的Module，並使之包含一個內聚的概念集合。這通常會實作Module之間的低耦合，但如果效果不理想，則應尋找一種更改模型的方式來消除概念之間的耦合。
> Module的名稱應該是Ubiquitous Language中的術語。Module及其名稱應反映出領域的深層知識。


- 當模組間無法避免耦合時，務必確保他們之間的依賴關係是非循環的。
- 父模組與子模組也應盡量避免循環依賴，但像是父模組建立子模組，子模組參考引用父模組的話可以允許。
- 模組不是模型的靜態概念，應該讓模組與其構成物件一起建模。


要建模一間廚房，會自然地想建立一個模組叫「餐具抽屜」，裡面會包含叉子、湯匙、刀子等物件，甚至可以考慮把餐巾放入，才不會看起來像是金屬類的餐具抽屜。
實際上，建立尖銳的、舀東西的、鈍器等模組並沒有太大幫助。

我們考慮的是用途，這會有助於模組的設計。

## 模組命名的基本規則

一般會以企業行號或組織的名稱作為開頭，包含網路上的網域名稱。
如果採用網域名稱，則順序上通常會以最上層的域名為先、然後才是該組織單位本身的域名。

```
com.saasovation // Java
SaaSOvation // C#
```

## 模型模組的命名規範

模組名稱的下一個結構，可以識別出其所屬的Bounded Context，在這一層加入Bounded Context的名稱是有好處的。
並在名稱後面加上domain關鍵字。

```
com.saasovation.identityaccess.domain
com.saasovation.collaboration.domain
com.saasovation.agilepm.domain
```

這種規範同時適用於傳統的分層架構與六角架構。

但domain通常僅只作為一個容器，用於打包更往下層的模組。
```
com.saasovation.identityaccess.domain.model
```
從這一層開始，才會加入實際的模型類別定義，就以這一層來說，可能會是用於安置可供重複利用的介面與抽象類別。
```
ConcurrencySafeEntity
DomainEvent
DomainEventPublisher
DomainEventSubscriber
DomainRegistry
Entity
IdentifiedDomainObject
IdentifiedValueObject
```

如果想將領域服務與domain.model劃分在不同模組中：
```
com.saasovation.identityaccess.domain.service
```

## 敏捷是專案管理情境中的模組
三個頂層模組：tenant, team, product

```
com.saasovation.agilepm.domain.model.tanant
	<<value object>> TanantId
```
幾乎所有模型中其他的模組或物件都依賴於它；換言之，這個模組的關鍵就在於將租戶物件彼此之間的依賴給清楚切割開來。所有對此模組的依賴都是單向的。

```
com.saasovation.agilepm.domain.model.team
	<<service>> MemberService
	<<aggregate root>> ProductOwner
	<<aggregate root>> Team
	<<aggregate root>> TeamMember
```
在Team這個類別中，擁有一個ProductOwner實例，以及一個持有任意數量TeamMember實例的集合，這兩個實例則是透過MemberService所產生。這三個聚合的聚合根實體，都參照了tenant模組中的TenantId。
```java
package com.saasovation.agilepm.domain.model.team;
import com.saasovation.agilepm.domain.model.tenant.TenantId;
public class Team extends ConcurrencySafeEntity {
	private TenantId tenantId;
	...
}
```

MemberService算是位於防護層的最前線，用於同步更新開發團隊成員在「身份與存取情境」中的識別、角色等設定，這個同步的動作是在背景處理的，與一般使用這請由無關。

在「敏捷式專案管理情境」中有一個product的父模組，旗下包含三個子模組：
```
com.saasovation.agilepom.domain.model.product
	<<aggregate root>> Product
	...
	com.saasovation.agilepm.domain.model.product.backlogitem
		<<aggregate root>> BacklogItem
		...
	com.saasovation.agilepm.domain.model.product.release
		<<aggregate root>> Release
		...
	com.saasovation.agilepm.domain.model.product.sprinte
		<<aggregate root>> Sprint
		...
```
這也是Scrum情境的核心模型所在，其中有Product, BacklogItem, Release, Sprint等聚合。

團隊在考量時，優先選擇模組的組織結構而非模組間的耦合關係。

```java
package com.saasovation.agilepm.domain.model.product;

import com.saasovation.agilepm.domain.model.tentan.TenantId;

public class Product extends ConcurrencySafeEntity {
	private ProductId productId;
	private TeamId teamId;
	private TenantId tenantId;
	...
}
```

```java
package com.saasovation.agilepm.domain.model.backlogitem;

import com.saasovation.agilepm.domain.model.tentan.TenantId;

public class BacklogItem extends ConcurrencySafeEntity {
	private BacklogItemId backlogItemId;
	private ProductId productId;
	private TeamId teamId;
	private TenantId tenantId;
	...
}
```

backlogitem與product模組之間實際上是雙下依賴的，幸好這三個子模組是作為product的子模組存在，因此依賴管理原則可以在這一點上稍微放鬆。同樣是以組織結構為重，耦合問題次之為考量。



## 其他架構層中的模組

### 分層架構

#### 使用者介面層，支援RESETful
```
com.saasovation.agilepm.resources
com.saasovation.agilepm.resources.view
```

#### 應用程式層
以一種服務對應一個模組的方式劃分
```
com.saasovation.agilepm.application.team
com.saasovation.agilepm.application.product
com.saasovation.agilepm.application.tenant
```

以「身份與存取情境」來說，由於當下應用服務的數量還不多，因此以一個主要的模組容納所有服務
```
com.saasovation.identityaccess.application
```


## 模組優先，Bounded Context在後
若術語不夠清新，不清楚該不該建立Boudned Context時，可以先試試將所有東西放在一起。此時，便可以運用模組作為輕量化的邊界、而非直接建立生硬不可踰越的情境界線。

Bounded Context並不是用來取代模組的，而模組的存在，是為了將高內聚性的領域物件給模組化，並將那些內聚成度不高的物件彼此分隔開來。