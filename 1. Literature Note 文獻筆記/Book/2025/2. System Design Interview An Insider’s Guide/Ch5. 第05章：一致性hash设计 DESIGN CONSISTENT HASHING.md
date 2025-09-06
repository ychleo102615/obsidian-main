---
tags: 
date: 2025-06-26
time: 21:56
link: https://github.com/Admol/SystemDesign/blob/main/CHAPTER%2005：DESIGN%20CONSISTENT%20HASHING.md
---
#### 再哈希问题


如果你有n个缓存服务器，平衡负载的一个常用方法是使用以下哈希方法：

$serverIndex=hash(key)modN$，其中N是服务器池的大小

当服务器池的大小是固定的，而且数据分布均匀时，这种方法效果很好。

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-1.jpg)

##### 如果server1 下線了呢？

大多数键都被重新分配，而不仅仅是最初存储在脱机服务器（服务器1）中的键。 这意味着，当服务器1离线时，大多数缓存客户会连接到错误的服务器来获取数据，这就造成了高速缓存失误的风暴。一致性哈希是一种有效的技术来缓解这个问题。
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-2.jpg)


#### 一致性哈希

引用自维基百科：“一致性哈希是一种特殊的哈希，当重新调整哈希表的大小并使用一致性哈希时，平均只需要重新映射 k/n 个键，其中 k 是键的数量， n 是槽的数量。 相比之下，在大多数传统的哈希表中，数组槽数量的变化导致几乎所有键都被重新映射 ”

#### 哈希空间和哈希环
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-3.jpg)       

![300](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-4.jpg)


#### 哈希服务器  Hash servers

使用相同的哈希函数 f，我们根据服务器的 IP 或名称将服务器映射到环上。 图 5-5 显示哈希环上映射了 4 个服务器


![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-5.jpg)
#### 服务器查找

为了确定键存放在哪个服务器上，我们从键在环上的位置顺时针查找，直到找到一个服务器。 图5-7解释了这个过程。顺时针方向查找，`key0`存储在`server0`；`key1`存储在`server1`；`key2`存储在`server2`，`key3`存储在`server3`。
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-7.jpg)


#### 添加一台服务器

使用上述逻辑，增加一台新的服务器将只需要重新分配一部分的键。

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-8.jpg)

#### 移除一台服务器

当一台服务器被移除时，只有一小部分的键需要用一致的哈希法进行重新分配。
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-9.jpg)



#### 基本方法中的两个问题

1. 首先，考虑到可以添加或删除服务器，**不可能保持环上所有服务器的分区大小相同**。
2. 在环上有可能出现**不均匀的键分布**。

**一种叫做虚拟节点或复制的技术被用来解决这些问题**
#### 虚拟节点

虚拟节点指向真实节点，每个服务器由环上的多个虚拟节点表示。在图5-12中，server0和server1都有3个虚拟节点。 3是任意选择的；而在现实世界的系统中，虚拟节点的数量要大得多。

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter5/figure5-12.jpg)

对于一两百个虚拟节点，标准偏差在均值的 5%（200 个虚拟节点）和 10%（100 个虚拟节点）之间。 当我们增加虚拟节点的数量时，标准偏差会更小。 但是，需要更多空间来存储有关虚拟节点的数据。 这是一个权衡，我们可以调整虚拟节点的数量以满足我们的系统要求。
[https://tom-e-white.com/2007/11/consistent-hashing.html](https://tom-e-white.com/2007/11/consistent-hashing.html)




一致性哈希的好处包括：

- 当服务器被添加或删除时，很小一部分的键被重新分配。
- 容易水平扩展，因为数据分布更加均匀。
- 缓解热点健问题。 对特定分片的过度访问可能会导致服务器过载。 想象一下 Katy Perry、Justin Bieber 和 Lady Gaga 的数据最终都在同一个分片上。 一致性哈希通过更均匀地分配数据来缓解这个问题。

一致性哈希广泛用于现实世界的系统，包括一些著名的系统：

- 亚马逊 Dynamo 数据库的分区组件 
- Apache Cassandra 中跨集群的数据分区 
- Discord 聊天应用
- Akamai 内容分发网络
- Maglev 网络负载均衡器 