---
tags: 
date: 2025-05-18
time: 21:30
link: https://github.com/Admol/SystemDesign/blob/main/CHAPTER%2001：SCALE%20FROM%20ZERO%20TO%20MILLIONS%20OF%20USERS.md
---
持續精煉、無止盡的改進

# Single server setup

![500](https://github.com/Admol/SystemDesign/blob/main/images/chapter1/figure1.jpg?raw=true)
所有東西都在server裡面：web application, database, cache。

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure2.jpg)

1. 使用者透過域名訪問網站
2. 瀏覽器、app得到ip
3. 向web server傳送http request
4. web server返回 HTML Page 或 json

# Database
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure3.jpg)

### 要使用什麼資料庫？   有關係型資料庫和非關係型資料庫。
##### 關係型資料庫：relational database management system (RDBMS), SQL database
MySQL, Oracle database, PostgreSQL
我們可以對不同的表進行join

##### 非關係型資料庫：NoSQL database
CouchDB、Neo4j、Cassandra、HBase、Amazon DynamoDB
四個種類：key-value stores, graph stores, column stores, and document stores，不支持join操作

關係型資料庫已經存在很久了，通常是最好的選擇。但以下情況用另外一種可能比較好：
1. 應用需要超低延遲
2. 非結構化，或是沒有關聯資料
3. 你只需要序列與反序列化資料（JSON, XML）
4. 需要大量存儲

### 垂直擴展、水平擴展 Vertical scaling vs horizontal scaling

vertical: 增加單個server的能力（cpu, ram)
horizontal: 部署更多server

流量低時用垂直擴展就好。他的優點在於簡單。但他也有以下問題：
- 無法無限制地添加CPU, RAM
- 沒有故障轉移failover和冗餘redundancy，當機就會全死

目前的設計中，server倒了就倒了，而且使用者變多了之後，反應就會變慢，甚至連不上。
load balancer可以解決這些問題。

# 負載均衡器 Load balancer

load balancer會均勻分散流量給web server（集中定義在load-balanced set）
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure4.jpg)


- 如果server1倒了，還有server2維持服務，並且要在新增一個server
- 如果流量增長下去，那就加入更多server

# 資料庫複製 Database replication
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure5.jpg)

master負責寫入，slave負責讀取。通常read的需求比write來得大的多。

- 更高的性能
- 更可靠，如果單個資料庫損毀還有其他的
- 高可用性（high availability），即使一台斷線，也有其他的可以使用

如果database斷線怎麼辦？
- 只有一個slave斷線的話，就暫時讓master也負責read，並且補上新的。多個slave的話就將read導向其他slaves
- 如果master斷線的話，就推舉一個slave成為新master，要注意新master有可能資料遺失 [[5. Replication#Leader failure Failover]]


![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure6.jpg)



# 緩存 Cache

每次讀取資料很慢，所以把資料存在記憶體裡，以便更快處理。

### 緩存層 Cache Tier 
![800](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure7.jpg)

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure7-8.jpg)


#### 使用緩存該考慮的事
- 常讀但不常修改就很適合用
- 過期策略：太短導致資料重複加載，太長導致資料過時
- 一致性問題：資料與緩存不會馬上同步，因為他們的修改不在同一個transaction中 （參考“Scaling Memcache at Facebook” published by Facebook）
- 減少故障：避免A single point of failure (SPOF)，最好在多個資料中心配置多個緩存。配置比需要大小還要高一定百分比的內存
- 驅逐策略 Eviction Policy：Least-recently-used (*LRU*),  Least Frequently Used (*LFU*), First In First Out (*FIFO*)


# Content delivery network (CDN)

在分散的地理位置上，傳遞靜態的內容：圖片、影片、CSS、JavaScript

![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure9.jpg)

用途就是要找一個比較近的地方拿資料。

![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure10.jpg)


#### 使用CDN該考慮的事
- CDN要錢，由第三方提供
- 設置適當的過期時間
- CDN fallback：CDN失效時，要能夠向源頭請求資源
- 使用api使資源失效，或是管理版本

![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure11.jpg)


# 無狀態Web層  Stateless web tier
將狀態移出網路層（到資料庫）。

#### 有狀態架構
![650](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure12.jpg)

這麼做的缺點是每次連線都得連到同一台server。可以透過sticky session辦到，但就是有額外開銷，也不好新增刪除server。

#### 無狀態架構
![650](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure13.jpg)

狀態資料可以透過共享的存儲取得。
這使一個無狀態的系統更簡單、更堅韌、可擴展。

![650](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure14.jpg)

共享的資料可以用關係型資料庫、Redis、NoSQL。 這裡選擇NoSQL是因為他比較容易擴展。

# 數據中心 Data center
從load balancer之後的架構就是data center

![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure15.jpg)

可能會發生事情導致data center失效，此時需要另一個data center承接本來的流量

![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure16.jpg)

有幾個技術挑戰：
1. 導流的工具，例如GeoDNS
2. DataCenter彼此同步的問題
3. 在不同位置部署測試你的網站、應用


# 消息佇列 Message Queue
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure17.jpg)

這讓producer, consumer之間解耦

這是一個處理圖片的使用情境，剪裁、鋭化、模糊等工作需要時間來完成。消息佇列讓我們能以非同不的方式完成。
producer, consumer可以獨立擴展。

如果佇列變太大，我們可以擴展worker以減少處理時間；反之佇列小的話減少worker。
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure18.jpg)





# 日誌、指標、自動化 Logging, metrics, automation

##### 日誌
有助於監控、辨識錯誤與問題

##### 指標
幫助了解業務洞察以及系統健康狀態

主機：CPU、記憶體、磁碟
聚合層級指標：database, caches    （將來自多個個體（如多台伺服器、節點、請求）的數據彙總起來，形成「整體系統層級」的指標。）

##### 自動化
持續整合，構建、測試、部署


### 添增消息佇列及不同的工具

![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure19.jpg)


# 資料庫擴展 Database Scaling

### 垂直擴展
升級硬體來實踐，但是有不少缺點：
1. 昂貴
2. 單點失效
3. 無法應付大量使用者

### 水平擴展

也被稱為分區，彼此獨立不重疊。
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure20.jpg)


使用`userid % 4`  作為hash function來尋找分區
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure21.jpg)  ![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure22.jpg)



分區也增加了複雜度：
##### 重新分配 Resharding Data
盡量使資料分布均勻
[[6. Partitioning 分區#Rebalancing Partitions]]

##### 名人問題
避免他們擠在同一個分區

##### 連接與去範式化 Join and de-normalization
Denormalization 是在無法跨 shard 做 join 時的權衡做法，透過冗餘資料讓查詢能夠只依靠單表完成，提升效能與簡化實作。
[[10. Batch Processing#Reduce-Side Joins and Grouping]]

![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter1/figure23.jpg)