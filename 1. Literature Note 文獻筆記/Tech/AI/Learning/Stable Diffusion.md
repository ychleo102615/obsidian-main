---
tags: 
date: 2023-09-18-週一
time: 16:28
---
[hugging face](https://huggingface.co/blog/stable_diffusion)
其他中文[blog](https://www.cijiyun.com/newsview?id=449)
[latent diffusion git](https://github.com/CompVis/latent-diffusion)
[notebook](https://github.com/huggingface/notebooks/tree/main/diffusers)
[李宏毅yt](https://www.youtube.com/watch?v=JbfcAaBT66U&t=315s)
[stable-diffusion-art](https://stable-diffusion-art.com/how-stable-diffusion-work/)
[圖解Stable Diffusion](https://jalammar.github.io/illustrated-stable-diffusion/)


> [!cite]
> Stable Diffusion is based on a particular type of diffusion model called **Latent Diffusion**


三個重要的元素：
1. An autoencoder ([[Variational Auto-encoder|VAE]]).
2. A [U-Net](https://colab.research.google.com/github/huggingface/notebooks/blob/main/diffusers/diffusers_intro.ipynb#scrollTo=wW8o1Wp0zRkq) ([[Diffusion Model]]).
3. A text-encoder, _e.g._ [CLIP's Text Encoder](https://huggingface.co/docs/transformers/model_doc/clip#transformers.CLIPTextModel).

透過在去噪的過程中，加入文字去影響這之間神經網路的注意力，達到控制圖像生成。
關鍵字是 **text conditioned latent unet**。
[text-to-image](https://eugeneyan.com/writing/text-to-image)
![](https://eugeneyan.com/assets/stable-diffusion.jpg)

注意黃色區塊，使用的是 [[Cross Attention]]。

[[2023-09-12|2023-09-12-週二, 15:11]]
## What is CFG value?
Classifier-Free Guidance.
這個數值會影響text prompt多大程度的影響擴散過程。

[link](https://stable-diffusion-art.com/samplers/)
This **denoising process** is called **sampling**

## [Samplers](https://stable-diffusion-art.com/samplers/)
#### h5同事介紹
[slides](https://docs.google.com/presentation/d/1_NMjis5a3asJGwPa-o70YippSuQDxuzg_pCc2CmQUf8/edit?pli=1#slide=id.g246243efd1b_0_0)
[intall](https://docs.google.com/presentation/d/1VDRfpaTMGHXMNpxjkTmxwjVKpxb15EMwQQK_bWgo4EI/edit#slide=id.g244487a9972_1_116)

[install link](https://blog.jimmycstudio.com/stablediffusion-local-install/)
[mac install](https://updayday.notion.site/MacOS-Stable-Diffusion-WebUI-M1-M2-Intel-61a0fd82ea0e451d9ead16beafc3a28b)

# WebUI

### 插件
- [tag autocomplete](https://github.com/DominikDoom/a1111-sd-webui-tagcomplete)
- [controlnet](https://github.com/Mikubill/sd-webui-controlnet)

### 公司電腦prompt
```shell
export COMMANDLINE_ARGS="--medvram --opt-split-attention --skip-torch-cuda-test --no-half"
```

## Models
[推薦model](https://blog.256pages.com/best-3-realistic-model-stable-diffusion/)
[game icon](https://civitai.com/models/47800?modelVersionId=76533)

### 為什麼Stable Diffusion可以產生不同尺寸的圖片？
[ref](https://blog.runpod.io/why-altering-the-resolution-in-standard-diffusion-gives-strange-results/)
他應該是利用將多個 cell 拼組成指定圖示尺寸的方式來達成的。

## Extra Reading
[image size](https://linuxhint.com/what-image-size-best-stable-diffusion/)
[Introduction to Diffusion Models for Machine Learning](https://www.assemblyai.com/blog/diffusion-models-for-machine-learning-introduction/)
[How physics advanced Generative AI](https://www.assemblyai.com/blog/how-physics-advanced-generative-ai/#generative-ai-with-thermodynamics)
