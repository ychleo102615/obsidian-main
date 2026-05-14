---
tags: []
date: 2026-05-14
time: 16:26
---

重複利用 path

```css
<defs>
    <path
        id="path-template
        d="..."
    >    
</defs>
```
想要重複利用的部分放在 defs 裡面。

```css
<use 
    href="#path-template"
/>
```


從教學上來看，感覺主要的好處在於節省 HTML 檔案大小。

問 AI 之後，他也有減少 DOM 節點數量、進而減少 Style Recalc 相關的運算。