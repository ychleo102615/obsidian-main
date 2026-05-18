---
tags: []
date: 2026-05-18
time: 12:07
link: https://courses.joshwcomeau.com/wham/animation-design/02.02-boop
---

講師示範了兩種 hover 模式：
第一種：hover 時會停在那裡
第二種：hover 時觸發一個效果動畫，結束後回到本來的狀態

講師稱呼第二種為 boop 動畫，像是在點狗狗鼻子。

使用的技巧：

### 用 hover + keyframes
這會有中斷效果，比較突兀。

### 自訂屬性 + transition

不用 hover ，而是一個自訂屬性，例如：`--is-booped` 來表示狀態。
動畫用 listener 觸發添增 `--is-booped`，但是要自己計時刪除。