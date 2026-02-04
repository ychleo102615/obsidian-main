---
tags: 
date: 2025-06-22
time: 12:46
link: https://github.com/Admol/SystemDesign/blob/main/CHAPTER%2002：BACK-OF-THE-ENVELOPE%20ESTIMATION.md
---
在系統面試中，你可能需要粗估系統的容量以及表現。

# 2的幂次方 Power of two

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter2/table2-1.png)

# 每个程序员都应该了解的延迟数据 Latency numbers every programmer should know

Google的Dean博士在2010年透露了典型计算机操作的时间。 随着计算机变得更快更强大，一些数字已经过时。然而，这些数字仍然应该能够让我们了解不同计算机操作的速度和慢速。

![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter2/table2-2.png)

[每个程序员都应该知道的延迟数据](https://colin-scott.github.io/personal_website/research/interactive_latency.html)
![600](https://github.com/Admol/SystemDesign/raw/main/images/chapter2/figure2-1.png)

- 内存速度快，但磁盘速度慢。
- 如果可能的话，应避免磁盘寻道。
- 简单的压缩算法速度快。
- 在发送数据到互联网之前，尽可能对数据进行压缩。
- 数据中心通常位于不同的区域，发送数据之间需要一定的时间。


# 可用性数据 Availability numbers
![500](https://github.com/Admol/SystemDesign/raw/main/images/chapter2/table2-3.png)

