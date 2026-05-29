---
tags: []
date: 2026-05-29
time: 21:58
---

## Applying transforms to view transition layers

在做本章的[練習題](https://courses.joshwcomeau.com/wham/03-advanced-interactions/07.03-vt-exercises)時，遇到非常詭異的問題：view-transition-group 會往左上角飛去。

#### 第一個解法：
當時講師提供的解決方法是使用 view-transition-old/new。
我後來問 ai 才知道，view-transition-old/new 是 view-transition-group 的子元素。

原本 group 的方式，是會用到線性插值。所以目前的位置與目標 translate 的位置（算錯到左上角）會變的不符合預期。
而 old/new 就是單純相對於 group 容器在移動而已。


#### 第二個解法：
```css
::view-transition-group(my-element) { animation-composition: add; }
```