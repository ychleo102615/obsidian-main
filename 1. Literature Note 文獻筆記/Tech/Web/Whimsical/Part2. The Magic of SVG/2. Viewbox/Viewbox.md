---
tags: []
date: 2026-05-14
time: 11:22
---
前一章的內容，SVG 元素繪製的位置都是絕對的比例。
如果 width 不夠的話，會把超出部分 crop 掉。

我們更期待 img 元素可以配合 element size 放大縮小。

動態調整內部數據（cx, cy, r, stroke-width....） 雖然可行，但是非常不推薦。

##### `viewbox` 屬性定義了內部的座標系統。
或者說 viewbox 定義了內部座標要暴露給外部繪製的窗口。

view box 的作用與 view port 其實很像。