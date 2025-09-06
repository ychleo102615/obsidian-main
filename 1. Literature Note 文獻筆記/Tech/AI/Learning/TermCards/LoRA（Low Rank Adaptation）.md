---
tags: 
date: 2023-09-12-週二
time: 16:03
---
[stable-diffusion-art](https://stable-diffusion-art.com/lora/)
[hugging face](https://huggingface.co/docs/diffusers/training/lora)
[HF Blog](https://huggingface.co/blog/lora)
[training](https://huggingface.co/docs/diffusers/training/lora)
[deep dive](https://www.ml6.eu/blogpost/low-rank-adaptation-a-technical-deep-dive)
[原作者git](https://github.com/cloneofsimo/lora#lengthy-introduction)
[論文](https://arxiv.org/pdf/2106.09685.pdf)

## 為什麼要使用LoRA
一般來說，我們想要對model進行 Fine-tunning，來達成不同的客製化需求。但是Fine-tunning的成本高，訓練過程以及結果都很笨重（速度慢、難以抓平衡、結果資料量大）。
LoRA可以用規模更小的方式進行Fine-tunning

藉由修改 [[Cross Attention]]，達到效果。

Cross Attention架構的所有權重，我們可以想像他們用矩陣來表示。
舉例來說，現在有一個`1000 * 2000`的資料，等於有兩百萬筆。

那LoRA之所以可以用更小的資料達成同樣的效果，是因為它把本來這麼大的矩陣資料，用兩個小矩陣（low rank）來表示。
```
1000 * 2 X 2 * 2000 = 1000 * 2000
```
這樣拆解之後，之需要六千筆資料，小了三百倍。

## 背後的原理
我們假設模型所處的空間，相對於我們想處理的問題，維度可能太高了。解決問題實際需要的空間維數可能更低，這被叫`Intrinsic Dimension 本徵維度`。
所以我們可以在更低維度的空間中，進行任務的學習。
[深度学习中的本征维度](https://zhuanlan.zhihu.com/p/612630431)

### 套用lora
```Python
pipe.unet.load_attn_procs(model_path)
```

LoRa 和 Stable Diffusion 可以一起運作，以提高 Stable Diffusion 模型的生成圖像的質量和效率。LoRa 可以用來凍結 Stable Diffusion 模型的大部分權重，只對部分權重進行微調。這可以顯著減少 Stable Diffusion 模型的訓練時間和計算成本。
