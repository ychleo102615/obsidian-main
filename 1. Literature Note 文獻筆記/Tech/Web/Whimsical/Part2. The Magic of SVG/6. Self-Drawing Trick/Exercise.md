---
tags: []
date: 2026-05-14
time: 17:49
link: https://courses.joshwcomeau.com/wham/02-svg/07.01-self-drawing-exercises
---
## Self-drawing swoop

```css
.foreground {
    stroke-dasharray: 100, 1000;
    stroke-dashoffset: 100px;
}
button:hover .foreground {
    stroke-dashoffset: 0px;
}
@media (prefers-reduced-motion: no-preference) {
    .foreground {
        transition: stroke-dashoffset 750ms;
    }
}
```

我最初還想要使用 `button.addEventListener('mouseover)`
來操作，並且用 keyframes。

但是就功能語意上來說，用 keyframes 完全不適合（應該說用起來會太麻煩）。
這裡的動畫涉及狀態切換，適合使用 transition。


## Circular Progress Indicator

pageLength 雖然是 presentation attribute ，但是他無法用 CSS property 來設置（只能用 attribute）。

另外，[[Transform Origins]] 可以用來旋轉圖形。之前眨眼的練習題有有苦戰過。
```css
transform-origin: center;
```


## Electrical Wiring

這題練習我做了很久，而且可能多繞了許多路。

我做了一限制：dash + gap 總和得是 total length。
並且據此調整 dash, gap 的長度。

|      | dash | gap              |
| ---- | ---- | ---------------- |
| from | 10   | totalLength - 10 |
| to   | 20   | totalLength - 20 |

這麼做的原因是希望 offset 在推進的時候，內容物也剛好是總長。
原因下段說明。

起始位置隨機的做法，我是讓 offset 隨機一個數字，並且讓他循環跑 offset -> totalLength + offset 的做法。頭尾要對得上的話，就需要 dash + gap 總長與 totalLength 相同。

但是解答的做法就單純許多，隨機起始延遲時間而已。
但是光是這樣就省下上面的許多功法。

解答 dash gap 中的 gap 是固定一個大數字。
offset 也是單純 0 -> totalLength。
所以循環的起始點，必定會把 dash 繪製在頭部。
這題也有起始圖像（王冠、西瓜的小圖）可以擋住，所以也看不出破綻。

而我特意顛倒 dash, gap 的做法，在解答中的做法中也不需要了。
```css
stroke-dasharray: "0 10 10 0"
```


反思：我的想法常常有為了達成特殊要求或限制，而改的比較複雜的傾象。