---
tags: []
date: 2023-09-07-週四
time: 16:59
---

一般在指「**Denoising Diffusion Probabilistic Models**」。
[HF實作程式碼](https://huggingface.co/docs/diffusers/using-diffusers/write_own_pipeline)
[說明](https://huggingface.co/blog/annotated-diffusion)
[李宏毅yt](https://www.youtube.com/watch?v=ifCDXFdeaaM)


> [!NOTE]
> 原理簡單來說就是對dataset的圖片不斷加上Gaussian Noise，讓原本的圖片逐漸變成完全的雜訊。而模型的主要工作就是想辦法把雜訊修復回原圖，在訓練後就能透過輸入隨機雜訊來生成圖片。


## 讓神經網路學習：如何從純粹的噪音中（pure noise）逐漸去噪的過程。

![](https://huggingface.co/blog/assets/78_annotated-diffusion/diffusion_figure.png)


## 如何訓練Diffusion model
[tutorial](https://huggingface.co/docs/diffusers/tutorials/basic_training)
[notebook](https://colab.research.google.com/gist/anton-l/f3a8206dae4125b93f05b1f5f703191d/diffusers_training_example.ipynb#scrollTo=584739c5-83f5-4077-8379-89a7c9ff1bf2)
