---
tags: []
date: 2026-05-12
time: 21:56
link: https://courses.joshwcomeau.com/wham/01-particles/12.03-colors
---

使用隨機顏色時，比起在 RGB 三個位度上個別隨機，不如使用 HSL 。

這樣就能在隨機中保留了某種規則性，看起來會更整齊或是更能滿足特性效果。

文中只隨機 H 維度時，營造了一種粉蠟筆色調的感覺。

有種希望自己可以早點知道的感覺。


這邊意外知道另一種顏色表示法：
```
oklch()
```
雖然講者說不喜歡，但我覺得還不錯。



## Color Shifting

```css
@keyframes colorShift {
	from {
		background: var(--from-color);
	}
}
.particle {
	background-color: var(--to-color);
	animation: colorShift 1500ms linear;
}
```

這樣的顏色轉移有問題。因為動畫線性插值會在 RGB 空間上跑，所以過度的顏色與 HSL 建立的直覺不符，顏色會變灰調。


 [“Make Beautiful Gradients”](https://www.joshwcomeau.com/css/make-beautiful-gradients/)
