---
tags: []
date: 2026-05-14
time: 12:38
---
`A` command

```css
<path
    d="
        M [start-x],[start-y]
        A [rx],[ry] [rotation] [large-arc-flag] [sweep-flag] [end-x],[end-y]
        "
/>
```

arcs 的心理意象是在起點和終點之間，使用圓圈的邊緣作為其路徑。這就像是一顆球卡在一個洞上面，從側面來看，其底部的弧線。

`large-arc-flag`：走短邊使用 0，走長邊用 1。
`sweep-flag`：逆時鐘 0 ，順時鐘 1。

所有參數不可省略。