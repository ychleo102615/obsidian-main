---
tags: 
date: 2023-09-12-週二
time: 16:28
---
## Cross Attention
[ref](https://blog.csdn.net/MengYa_Dream/article/details/126688503)
就像Transformer裡面看到的 [[self-attention]]，會利用QKV來計算「相似分數」，但不同的是，向量的資料來源不一樣。
如果使用場景是用文字找圖的話，Q就會是文字向量，KV就是圖的向量了吧。
注意像圖、音檔這樣的向量，會需要降維處理。

[[2023-09-26|2023-09-26-週二, 10:33]]
後來想到了，文本和圖像不可能同一個維度，這邊要怎麼處理？
[ref](https://vaclavkosar.com/ml/cross-attention-in-transformer-architecture)
應該是要讓他們降維到一個維度，再執行cross attention

> [!NOTE] Title
> -multimodal input sequences (e.g. image, text, audio) into a low dimensional latent sequence
