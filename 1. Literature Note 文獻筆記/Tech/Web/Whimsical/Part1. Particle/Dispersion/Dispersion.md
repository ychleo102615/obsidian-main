---
tags: []
date: 2026-05-08
time: 00:11
link: https://courses.joshwcomeau.com/wham/01-particles/04-dispersion
---
這個章節在做粒子向外移動的動畫。

它首先挑戰我們自己實踐一個版本。

我做的版本是用 transform 的，講師用的是 left, top 百分比版本。我認為我的效能會比較好。
但是我忘記考慮到 -50% 的置中了。

我學到的東西：

#### 不同的動畫時間要怎麼設定
我自己查的時候，得到的答案是用逗號區隔就可以了。這挺直覺。
但是講師認為這樣不好，因為我們改動動畫順序的話，這邊就會出問題了。
這很有道理。

所以講師採用的方法是 CSS 變數。

### 位置設定
這很 tricky。也有用到 [[Partial Keyframes]] 的感覺。
keyframes 設定只設定 from 。
但是用 inline 的方式設定目標位置 `to`。

剛剛誤會他使用的是 `requestAnimationFrame`，這個是 transition 時才會用的技巧。