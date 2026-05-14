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