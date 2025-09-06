---
tags: 
date: 2023-09-13-週三
time: 17:17
---

VAE是 [[Stable Diffusion]] 中壓縮資料重要的一環。使用普通 [[Auto-encoder]] 訓練出來的模型會有盲點，即是解壓縮一任意資料，出來的資料可能是不明所以、沒有意義的。（或是說會造成overfitting）。VAE 可以解決這個問題，它將資料 **x** 先 encode 成潛在空間中的概率分布 **p(z|x)**，這賦予了連續性以及完整性。再從潛在空間中的概率分佈 **p(z|x)** 取樣出資料 **z** ，可以被 decode 回正常的資料 **x^**。

[Understanding Variational Autoencoders (VAEs)](https://towardsdatascience.com/understanding-variational-autoencoders-vaes-f70510919f73)
[Difference between AutoEncoder (AE) and Variational AutoEncoder (VAE)](https://towardsdatascience.com/difference-between-autoencoder-ae-and-variational-autoencoder-vae-ed7be1c038f2)
[[Auto-encoder]]

## PCA  Principal components analysis
利用線性組合的方式降維，並盡量使資料相近。
也可以說是在尋找最佳的`linear subspace`，使所有資料的投影距離越小越好。

相當於只有一層 layer 的 [[Auto-encoder]]。

雖然理論上，我們有辦法將所有資料壓到最小（一維），並且不失真地回復資料。
但是有兩件事：
1. 這樣的壓縮方式不好理解
2. 即使在 latent space，我們需要資料盡量保持原有結構

如果上述的model真的實作出來，那今天在latent space隨機選一個點，會導致回復出的資料是一個不明所以的資料（overfitting）。

[[2023-09-18|2023-09-18-週一, 14:44]]
## **所以，如果我們不對學習過程管控的話，它會朝沒有規則、無法理解的方向去優化。**

> [!abstract] Definition
> **A variational autoencoder can be defined as being an autoencoder whose training is regularised to avoid overfitting and ensure that the latent space has good properties that enable generative process**

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*ejNnusxYrn1NRDZf4Kg2lw@2x.png)

![](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*83S0T8IEJyudR_I5rI9now@2x.png)


接下來就是概率分佈切進來的地方了。encoder 是以產生 µ (mean) 和 σ (variance) 為目的來訓練，再 sample 出真正存在於 latent space 的代表值。



[[2023-10-03|2023-10-03-週二, 10:08]]
## 實際應用
[How to use VAE](https://www.pcguide.com/apps/how-to/stable-diffusion-how-to-use-vae/)

> [!NOTE]
> **我們需要安裝VAE嗎？**
不用，一般model裡面就有包含VAE了。當人們在說安裝某版本的VAE時，是指安裝其他加強版本的VAE，或許可以帶來更好的表現。



