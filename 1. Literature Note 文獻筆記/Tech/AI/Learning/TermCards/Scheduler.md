---
tags: 
date: 2023-09-22-週五
time: 14:46
---
[link](https://blog.segmind.com/what-are-schedulers-in-stable-diffusion/)
也被叫做Sampler。

## Scheduler是什麼？
是UNet階段時的演算法，是去噪過程（desnoising process）的重要角色。


> [!abstract]
> The key to all these scheduler algorithms is to progressively perturb data with intensifying random noise (called the “diffusion” process).


> [!summary]
> schedulers control the progression and noise levels during the diffusion process, affecting the overall image quality, while samplers introduce random perturbations to the images, influencing the variation and diversity of the generated outputs.
