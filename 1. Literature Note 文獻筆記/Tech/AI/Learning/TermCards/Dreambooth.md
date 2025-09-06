---
tags: 
date: 2023-09-13-週三
time: 14:51
---
[link](https://dreambooth.github.io/)
[hugging face library](https://huggingface.co/sd-dreambooth-library)
[hf blog](https://huggingface.co/blog/dreambooth)
[medium](https://dreambooth.github.io/DreamBooth_files/high_level.png)


可以針對一個特定的主要對象做 FIne-tuning ，使這個客製化的 model 生成的圖片可以很準確地描繪出該對象。

所以他不像LoRa或是ControlNet那樣子來控制一個model生成圖示，而是自成一個新model。
## 使用方式
提示詞需要使用前綴，如：
`A [V] sunglasses in the jungle`
在這裡`sugglasses`就是主要對象。

在保留主要對象的情況下，Dreambooth可以：
- 渲染風格、視角、姿勢
- 屬性調整（e.g. `A [color] [V] color`）
- 佩戴妝飾


![](https://dreambooth.github.io/DreamBooth_files/high_level.png)
