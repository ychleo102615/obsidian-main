---
tags:
  - AI
date: 2023-09-04-週一
time: 15:59
---

https://huggingface.co/learn/nlp-course/chapter1/4?fw=pt#architecture-vs-checkpoints

深度學習說白了，就是很多層的演算法（所以才叫深度），加上很多的參數，組合成的黑箱子。

|名稱|說明|
|-|-|
|`Architectures`|指的就是這些很多層的演算法，是如何排列、串接、運作的。
|`CheckPoints`|指的就是這之間可以被訓練的參數，也可以說是權重（weights）。因為model訓練到一半時，你會想要儲存目前訓練的「狀態」（我它也可以理解成「快照」），方便日後練壞掉了可以回復（就像gitk的commit節點吧），所以才叫checkPoints吧。
|`Model`| 可以拿來指這整個組合起來的黑箱子，或是上述的其中一個概念。


