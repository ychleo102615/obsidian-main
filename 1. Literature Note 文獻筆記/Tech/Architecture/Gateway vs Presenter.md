---
tags: []
date: 2025-03-26
time: 10:06
---
## **1. Gateway vs Presenter 在 WebSocket / MQ 中的角色**

|角色|主要职责|适用范围|重点关注|
|---|---|---|---|
|**Gateway**|处理协议（WebSocket、MQ 连接、事件订阅）|负责接收/发送数据，保持连接|**通信协议、事件管理**|
|**Presenter**|转换数据格式|只关注数据本身的格式|**数据格式化、结构转换**|

📌 **总结**：

- **Gateway 关注「怎么发送数据」**
    
- **Presenter 关注「数据长什么样」**

✅ Presenter **不只是 UI 层的概念**，它本质上是 **用来格式化 Use Case 输出数据** 的 Out Port。  
✅ Presenter 可以用于：

- **API 层（REST/gRPC）**
    
- **文件导出（CSV、Excel）**
    
- **消息队列（MQ/Kafka/RabbitMQ）**
    
- **WebSocket、实时数据流** ✅ 如果需要 **数据存取（数据库、外部 API 调用）**，那更适合用 **Out Port Adapter**。