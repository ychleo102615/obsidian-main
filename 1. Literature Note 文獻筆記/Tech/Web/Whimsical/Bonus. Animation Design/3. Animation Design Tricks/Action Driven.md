---
tags: []
date: 2026-05-18
time: 14:18
---

以動畫本身來驅動。
文中以 "open", "confirm", "cancel" 作為主要描述分類。

```css
.dialog {
    /* Hidden by default */
    transform: translateY(100%);
    
    &[data-action="open"] {
      transform: translateY(0);
      transition: transform 300ms;
    }
    &[data-action="cancel"] {
      filter: blur(10px);
      transform: translateY(100%) rotate(-20deg);
      opacity: 0;
      transition:
        transform 500ms,
        opacity 500ms,
        filter 500ms;
    }
    &[data-action='confirm'] {
      transform: translateY(100%);
      transition:
        transform 600ms cubic-bezier(0.54, -0.8, 1, 0.9);
    }
```

一個有趣的情境是，使用者快速 cancel 又 open 的話會怎麼樣？

這樣 open 時，面板會帶有最後的 cancel 狀態。其實快速切換的情境看起來挺直覺的，就像是 cancel 到一半又回復打開的狀態。
但是講師也提到，如果不是快速切換的情境，例如使用者去做別的事之後再回來看，發現還是帶有 cancel 狀態的話，會感覺比較微妙。

所以一個可行的做法會是，在 cancel 時，註冊計時器把 cancel class 移除掉。但是也要記得在 open 時要把這個計時器取消掉，否則會看到 cancel 被中斷的畫面。



對我來說，這有點像是繞了一大圈，用 CSS 的概念（declarative）來完成 imperative 的動畫。
但是 declarative 本身又有屬性描述的功能，所以也不是完全說 imperative 一定比較好。
