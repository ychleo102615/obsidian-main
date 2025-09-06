---
tags:
  - AI
date: 2023-09-05-週二
time: 15:28
---
## 什麼是 self-attention 自注意力機制？
#### 在處理Seq2Seq類型的model時，Self-attention可以去強調、弱化每個節點（這裡可以是詞彙、向量、像素....等連續性input的單位）之間彼此的關係（也就是調整權重），來達到更好的推導效果。


![](https://lh5.googleusercontent.com/8WL1hZqU56wcJzXcvfko7gR9CAcoaJu-0AEjUJCARtgFYoBJt7r9-tOUhQX8ceCbPuGpDSfcsJe7pSgELxScHsxcGnpb3I6Ha1V40oN4UdOb_Lj5Q6xhLD55vbfHELSRvDziAcI)

這張圖的範例在說明 `self-attention` 的計算過程。<br>圖中 a1 ~ a4 都代表一個向量，而每個向量又代表一個字（或是半個字），例如說「機器學習」。範例中 a2 經過 `self-attention` 計算後得到 b2，再接續進行其他的運算，如softmax（標準化資料）和feed forward neural network。

參考：
[post](http://violin-tao.blogspot.com/2021/12/ml-self-attention.html)
[李宏毅老師的yt影片 self-attention](https://www.youtube.com/watch?v=hYdO9CscNes)
[投影片](https://speech.ee.ntu.edu.tw/~hylee/ml/ml2021-course-data/self_v7.pdf)
