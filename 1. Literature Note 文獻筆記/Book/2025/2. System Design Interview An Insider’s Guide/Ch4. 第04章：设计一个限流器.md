---
tags: 
date: 2025-06-23
time: 21:46
link: https://github.com/Admol/SystemDesign/blob/main/CHAPTER%2004：DESIGN%20A%20RATE%20LIMITER.md
---

限制流量的好處：
1. 防止DoS攻擊
2. 降低成本，呼叫第三方api可能要錢
3. 減少負荷，防止過載


![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter4/figure4-1.jpg)

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter4/figure4-2.jpg)





在设计限流器时，要问自己的一个重要问题是：限流器应该在哪里实现，在服务器端还是在网关中？这没有绝对的答案。这取决于你公司目前的技术栈、工程资源、优先级、目标等。这里有一些通用的指南：

- 评估你目前的技术栈，如编程语言、缓存服务等。确保你目前的编程语言能够有效地在服务器端实现速率限制。
- 确定适合你业务需求的速率限制算法。当你在服务器端实施一切时，你可以完全控制算法。然而，如果你使用第三方网关，你的选择可能是有限的。
- 如果你已经使用了微服务架构，并在设计中包含了一个API网关来执行认证、IP白名单等，你可以在API网关上添加一个限流器。
- 建立你自己的速率限制服务需要时间。如果你没有足够的工程资源来实现限流器，商业API网关是一个更好的选择。



#### 限流算法

限流可以使用不同的算法来实现，每种算法都有其独特的优缺点。尽管本章并不关注算法，但在高层次上了解它们有助于选择正确的算法或算法组合来适应我们的使用情况。

下面是一个流行算法的列表：

- 令牌桶（Token bucket）
- 漏桶算法（Leaking bucket）
- 固定窗口计数器（Fixed window counter）
- 滑动窗口日志（Sliding window log）
- 滑动窗口计数器（Sliding window counter）


##### 令牌桶算法 
有一個容器裡面，每過一定時間可以獲得token。
當有request進來時，檢查有沒有token，有的話消耗token並接受請求，沒有的話捨棄請求。

令牌桶算法需要两个参数：
1. 桶大小：桶内允许的最大令牌数。
2. 填充速率：每秒放入到桶内的令牌数量。

**优点**

- 算法容易实现
- 占用内存少
- 令牌桶允许在短时间内进行突发流量。只要有剩余的令牌，请求就可以通过。

**缺点**

- 算法中有两个参数，即桶的大小和令牌的补充速率。然而，正确调整它们可能具有挑战性。

##### 漏桶算法

漏桶（Leaking bucket）算法与令牌桶类似，不同之处在于请求是以固定速率处理的。它通常用先入先出（FIFO）队列来实现。

![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter4/figure4-7.jpg)

**优点：**

- 鉴于队列大小有限，内存效率高。
- 请求以固定的速率处理，因此它适用于需要稳定流出速率的用例。

**缺点：**

- 突发的流量使队列中充满了旧的请求，如果这些请求没有得到及时处理，最近的请求将受到速率限制。
- 算法中有两个参数，要适当地调整它们可能并不容易。









![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter4/figure4-13.jpg)