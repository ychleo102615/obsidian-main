---
tags: 
date: 2025-07-06
time: 20:55
link: https://github.com/Admol/SystemDesign/blob/main/CHAPTER%2009：DESIGN%20A%20WEB%20CRAWLER.md
---
网络爬虫的基本算法很简单：

- 给定一组URLs，下载所有由URLs指向的网页。
- 从这些网页中提取 URL。
- 将新的 URL 添加到要下载的 URL 列表中。重复这3个步骤。

除了要向面试官澄清的功能之外，记下优秀网络爬虫的以下特征也很重要：

- 可伸缩性（Scalability）：网络非常大。那里有数十亿个网页。使用并行化网络爬行应该非常有效。
- 堅固性（Robustness）：网络充满了陷阱。错误的 HTML、无响应的服务器、崩溃、恶意链接等都很常见。爬虫必须处理所有这些边缘情况。
- 礼貌（Politeness）：爬虫不应该在短时间间隔内向网站发出太多请求。
- 可扩展性（Extensibility）：系统非常灵活，因此只需进行最少的更改即可支持新的内容类型。比如我们以后要抓取图片文件，应该不需要重新设计整个系统。

以下估算基于许多假设，与面试官沟通以达成共识很重要。

- 假设每月下载 10 亿个网页。
- QPS： 1,000,000,000/30天/24小时/3600秒=400页/秒。
- 峰值QPS=2×QPS=800
- 假设平均网页大小为 500k
- 10亿页×500k=每月500TB 存储空间。如果您对数字存储单元不清楚，请重新阅读第 2 章中的“2 的幂”部分。
- 假设数据存储五年， 500TB×12个月×5年=30PB。需要 30 PB 的存储来存储五年的内容。

![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-2.jpg)


#### Seed URLs

网络爬虫使用种子 URL 作为爬网过程的起点。例如，要抓取大学网站的所有网页，选择种子 URL 的一种直观方法是使用大学的域名。

要抓取整个网络，我们需要创造性地选择种子 URL。一个好的种子 URL 是一个很好的起点，爬虫可以利用它来遍历尽可能多的链接。一般的策略是将整个 URL 空间分成更小的空间。第一个提议的方法是基于位置的，因为不同的国家可能有不同的流行网站.

另一种方法是根据主题选择种子网址；例如，我们可以将 URL 空间划分为购物、体育、医疗保健等。种子 URL 选择是一个开放式问题，您不应该给出完美的答案，先大胆想想。

#### URL Frontier

大多数现代网络爬虫将爬行状态分为两种：待下载和已下载。存储待下载的URL的组件被称为URL Frontier。你可以把它称为先进先出（FIFO）队列。关于URL Frontier的详细信息，请参考深入研究的内容。

#### HTML Downloader

HTML Downloader 从互联网上下载网页。这些URL是由URL Frontier提供的。

#### DNS Resolver

要下载网页，必须将 URL 转换为 IP 地址。 HTML Downloader 调用 DNS Resolver 为 URL 获取相应的 IP 地址。例如，截至 2019 年 3 月 5 日，URL [www.wikipedia.org](http://www.wikipedia.org/) 已转换为 IP 地址 198.35.26.96。

#### Content Parser

下载网页后，必须对其进行解析和验证，因为格式错误的网页可能会引发问题并浪费存储空间。在爬网服务器中实现内容解析器会减慢爬网过程。因此，Content Parser（内容解析器）是一个单独的组件。

#### Content Seen?

在线研究显示，29%的网页是重复的内容，这可能导致同一内容被多次存储。我们引入了 "Content Seen? "数据结构，以消除数据的冗余，缩短处理时间。它有助于检测以前存储在系统中的新内容。为了比较两个HTML文档，我们可以逐个字符进行比较。然而，这种方法既慢又费时，特别是当涉及到数十亿的网页时。完成这项任务的一个有效方法是比较两个网页的哈希值。

#### Content Storage

它是一个用于存储HTML内容的存储系统。存储系统的选择取决于诸如数据类型、数据大小、访问频率、寿命等因素，磁盘和内存都被使用。

- 大部分内容存储在磁盘上，因为数据集太大而无法放入内存。
- 热门内容保存在内存中以减少延迟。

#### URL Extractor

URL Extractor（网址提取器） 从 HTML 页面解析和提取链接。图 9-3 显示了链接提取过程的示例。通过添加“[https://en.wikipedia.org](https://en.wikipedia.org/)”前缀将相对路径转换为绝对 URL。

![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-3.jpg)

#### URL Filter

URL Filter 排除某些内容类型、文件扩展名、错误链接和“黑名单”站点中的 URL。

#### URL Seen？

"URL Seen? "是一个数据结构，用于跟踪之前被访问过的或已经在Frontier中的URL。"URL Seen? "有助于避免多次添加相同的URL，因为这可能会增加服务器负载并导致潜在的无限循环。

布隆过滤器和哈希表是实现 "URL Seen? "组件的常用技术。我们不会在这里介绍布隆过滤器和哈希表的详细实现。欲了解更多信息，请参考参考资料

#### URL Storage

URL Storage 存储已经访问过的 URL。

### 网络爬虫工作流程

为了更好地逐步解释工作流程，在设计图中添加了序列号，如图 9-4 所示。
![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-4.jpg)

第 1 步：将种子 URL 添加到 URL Frontier
第 2 步：HTML 下载器从 URL Frontier 获取 URL 列表。
第 3 步：HTML 下载器从 DNS 解析器获取 URL 的 IP 地址并开始下载。
第 4 步：Content Parser 解析 HTML 页面并检查页面是否格式错误。
第 5 步：内容经过解析和验证后，传递给“Content Seen?”组件。
第 6 步：“Content Seen”组件检查 HTML 页面是否已在存储中。
- 如果在存储中，这意味着不同URL 中的相同内容已经被处理过。在这种情况下，HTML 页面将被丢弃。
- 如果不在存储中，则系统之前没有处理过相同的内容。内容被传递给链接提取器。
第 7 步：网址提取器从 HTML 页面中提取网址。
第 8 步：将提取的网址传递给 URL 过滤器。
第 9 步：网址过滤后，传递给“URL Seen?”组件。
第 10 步：“URL Seen”组件检查一个URL是否已经在存储中，如果是，则之前处理过，不需要做任何事情。
第 11 步：如果一个 URL 以前没有被处理过，它被添加到 URL Frontier。

接下来，我们将深入讨论最重要的构建组件和技术：

- 深度优先搜索 (DFS) 与广度优先搜索 (BFS)
- URL Frontier
- HTML Downloader
- 鲁棒性（Robustness）
- 可扩展性（Extensibility）
- 检测并避免有问题的内容


#### DFS vs BFS

你可以把网络想象成一个有向图，其中网页作为节点，超链接（URL）作为边。抓取过程可以被视为从一个网页到其他网页的有向图的遍历。两种常见的图形遍历算法是DFS和BFS。然而，DFS通常不是一个好的选择，因为DFS的深度可能很深。

BFS 通常被网络爬虫使用，并通过先进先出 (FIFO) 队列实现。在 FIFO 队列中，URL 按照它们入队的顺序出队。但是，这种实现有两个问题：

1. 来自同一网页的大多数链接都链接回同一主机。在图 9-5 中，[wikipedia.com](http://wikipedia.com/) 中的所有链接都是内部链接，使得爬虫忙于处理来自同一主机（[wikipedia.com](http://wikipedia.com/)）的 URL。当爬虫试图并行下载网页时，维基百科服务器将被请求淹没。这被认为是“不礼貌的”
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-5.jpg)

2. 标准的BFS没有考虑到一个URL的优先级。网络很大，不是每个页面都有相同的质量和重要性。因此，我们可能希望根据页面排名、网络流量、更新频率等来确定URL的优先级。


#### URL Frontier

URL Frontier 有助于解决这些问题。 URL Frontier 是一种存储要下载的 URL 的数据结构。 URL Frontier 是确保礼貌、URL 优先级和新鲜度的重要组成部分。参考资料  中提到了一些关于 URL Frontier 的值得注意的论文。这些论文的研究结果如下：

##### 礼貌性

一般来说，网络爬虫应该避免在短时间内向同一个托管服务器发送过多的请求。发送过多请求会被视为“不礼貌”，甚至被视为拒绝服务 (DOS) 攻击。例如，在没有任何限制的情况下，爬虫可以每秒向同一个网站发送数千个请求。这会使 Web 服务器不堪重负。

强制礼貌的一般想法是一次从同一主机下载一个页面。可以在两个下载任务之间添加延迟。礼貌约束是通过维护从网站主机名到下载（工作）线程的映射来实现的。每个下载线程都有一个单独的 FIFO 队列，并且只下载从该队列中获得的 URL。图 9-6 显示了管理礼貌的设计。

![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-6.jpg)
- Queue router：它确保每个队列（b1，b2，... bn）仅包含来自同一主机的 URL。
- Mapping table:：它将每个主机映射到一个队列

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/table9-1.jpg)

- FIFO 队列 b1、b2 到 bn：每个队列包含来自同一主机的 URL。
- Queue selector：每个工作线程都映射到一个 FIFO 队列，它只从该队列下载 URL。队列选择逻辑由Queue selector完成
- Worker thread 1 t到 N：一个工作线程从同一台主机上一个接一个地下载网页，可以在两个下载任务之间添加延迟。

##### 优先级

一个关于 Apple 产品的讨论论坛上的随机帖子与苹果主页上的帖子具有非常不同的权重。尽管它们都有 "Apple "这个关键词，但爬虫首先抓取 Apple 主页是明智之举。

我们根据实用性对 URL 进行优先级排序，这可以通过 PageRank 、网站流量、更新频率等来衡量。“Prioritizer”是处理 URL 优先级的组件。有关此概念的深入信息，请参阅参考资料 。

图 9-7 显示了管理 URL 优先级的设计。
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-7.jpg)

- Prioritizer：它将 URL 作为输入并计算优先级。 •
- Queue f1 到 fn:：每个队列都有一个分配的优先级。优先级高的队列被选中的概率更高。
- Queue selector：随机选择一个偏向于具有更高优先级的队列

图 9-8 展示了 URL frontier 设计，它包含两个模块：

- 前端队列：管理优先级
- 后端队列：管理礼貌

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-8.jpg)

#####  新鲜度
    网页不断被添加、删除和编辑。网络爬虫必须定期重新抓取下载的页面以保持我们的数据集最新。重新抓取所有 URL 既耗时又耗费资源。下面列出了几种优化新鲜度的策略：
    - 根据网页的更新历史重新抓取。
    - 对URL进行优先排序，优先和频繁地重新抓取重要页面。
	
#####  URL Frontier 存储
    在搜索引擎的真实世界抓取中，frontier 的 URL 数量可能达到数亿 [4]。将所有内容都放在内存中既不耐用也不可扩展。将所有内容都保存在磁盘中是不可取的，因为磁盘很慢；它很容易成为抓取的瓶颈。我们采用了混合方法。大多数 URL 都存储在磁盘上，因此存储空间不是问题。为了降低从磁盘读取和写入磁盘的成本，我们在内存中维护缓冲区以进行入队/出队操作。缓冲区中的数据会定期写入磁盘。

#### HTML 下载器

HTML下载器使用HTTP协议从互联网上下载网页。在讨论HTML下载器之前，我们先看一下Robots排除协议。

##### **Robots.txt**

Robots.txt，称为Robots排除协议，是网站用来与爬虫沟通的标准。它规定了爬虫可以下载哪些页面。在尝试爬行一个网站之前，爬虫应首先检查其相应的robots.txt，并遵守其规则。为了避免重复下载 robots.txt 文件，我们对该文件的结果进行了缓存。该文件会定期下载并保存到缓存中。下面是取自[https://www.amazon.com/robots.txt](https://www.amazon.com/robots.txt) 的robots.txt文件的一个片段。一些目录，如creatorhub，是不允许谷歌机器人访问的。

```httpspec
User-agent: Googlebot
Disallow: /creatorhub/*
Disallow: /rss/people/*/reviews
Disallow: /gp/pdp/rss/*/reviews
Disallow: /gp/cdp/member-reviews/
Disallow: /gp/aw/cr/
```

除了 robots.txt，性能优化是我们将为HTML下载器介绍的另一个重要概念。

##### **性能优化**

以下是HTML下载器的性能优化列表.

1. 分布式抓取

	为了实现高性能，抓取工作被分配到多个服务器，每个服务器运行多个线程。URL空间被分割成更小的部分；因此，每个下载器负责URL的一个子集。图9-9显示了一个分布式抓取的例子。
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-9.jpg)

2. 缓存DNS解析器
    DNS解析器是爬虫的一个瓶颈，因为由于许多DNS接口的同步性，DNS请求可能需要时间。DNS响应时间从10ms到200ms不等。一旦爬虫线程对DNS进行了请求，其他线程就会被阻断，直到第一个请求完成。维护我们的DNS缓存以避免频繁调用DNS是一种有效的速度优化技术。我们的DNS缓存保持域名到IP地址的映射，并通过cron作业定期更新。
	
3. 位置
    按地理分布抓取服务器。当爬行服务器离网站主机较近时，爬行者会体验到更快的下载时间。设计定位适用于大多数系统组件：抓取服务器、缓存、队列、存储等。
    
4. 短暂的超时
    
    有些网络服务器响应缓慢，或者根本不响应。为了避免漫长的等待时间，指定了一个最大的等待时间。如果一个主机在预定的时间内没有反应，爬虫将停止工作并抓取一些其他的网页。

#### 可靠性

除了性能优化，可靠性也是一个重要的考虑因素。我们提出了一些提高系统可靠性的方法。

- 一致性哈希：这有助于在下载者之间分配负载。 可以使用一致性哈希添加或删除新的下载服务器。 有关详细信息，请参阅第 5 章：设计一致性哈希。
- 保存爬行状态和数据：为了防止失败，爬行状态和数据被写入存储系统。 通过加载保存的状态和数据，可以轻松地重新启动中断的爬网。
- 异常处理：错误在大型系统中是不可避免的，也是常见的。 爬虫必须在不使系统崩溃的情况下优雅地处理异常。
- 数据校验：这是防止系统出错的重要措施。

#### 可扩展性（Extensibility）

差不多每个系统都在不断发展，设计目标之一是使系统足够灵活，以支持新的内容类型。抓取器可以通过插入新的模块来扩展。图9-10显示了如何添加新模块。

![700](https://github.com/Admol/SystemDesign/raw/main/images/chapter9/figure9-10.jpg)

- PNG下载器模块是用于下载PNG文件的插件。
- 增加了网络监控模块，以监控网络并防止版权和商标侵权。


#### 检测并避免有问题的内容

本节讨论冗余、无意义或有害内容的检测和预防。
1. 冗余内容
    如前所述，近30%的网页是重复的。哈希值或校验和有助于检测重复[11]。
    
2. 搜索引擎蜘蛛陷阱
    搜索引擎蜘蛛陷阱是导致爬虫陷入无限循环的网页。 例如，一个无限深的目录结构如下：`http://www.spidertrapexample.com/foo/bar/foo/bar/foo/bar/...` 可以通过设置 URL 的最大长度来避免此类蜘蛛陷阱。但是，不存在检测蜘蛛陷阱的万能解决方案。 包含蜘蛛陷阱的网站很容易识别，因为在此类网站上发现的网页数量异常多。 很难开发自动算法来避免蜘蛛陷阱； 但是，用户可以手动验证和识别蜘蛛陷阱，并从爬虫中排除这些网站或应用一些自定义的 URL 过滤器。
    
3. 垃圾数据
    有些内容价值很小或没有价值，例如广告、代码片段、垃圾邮件 URL 等。这些内容对爬虫没有用，应尽可能排除。