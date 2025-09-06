---
tags: 
date: 2023-09-21-週四
time: 14:54
---
[hugginFace tutorial](https://huggingface.co/blog/controlnet)
[learn opencv](https://learnopencv.com/controlnet/)
[github](https://github.com/lllyasviel/ControlNet#controlnet)
[論文](https://arxiv.org/pdf/2302.05543.pdf)
[知乎  原理、架構說明](https://zhuanlan.zhihu.com/p/608161469)
[stable diffusion art](https://stable-diffusion-art.com/controlnet/)
[download models](https://huggingface.co/lllyasviel/ControlNet-v1-1/tree/main)
[blog 安裝、大圖範例](https://blog.256pages.com/install-controlnet/)


## ControlNet是什麼？
它是一個neural network 架構，可以接受空間圖像資訊，來控制文轉圖的擴散模型

這是正常的 diffusion model ，x 代表輸入，y 代表輸出，Θ 代表神經網路的權重(checkpoints)。
```
y = F(x; Θ).
```

這是 controlNet版本的架構，Z 代表 `zero convolution` layers。
```
yc = F(x; Θ) + Z(F(x + Z(c; Θz1); Θc); Θz2),
```

> [!NOTE] 
> 零卷积(zero convolution):权重和偏置都是用0初始化的1 x 1卷积。

![](https://learnopencv.com/wp-content/uploads/2023/03/controlnet-before-after-stable-diffusion-connections.png)

