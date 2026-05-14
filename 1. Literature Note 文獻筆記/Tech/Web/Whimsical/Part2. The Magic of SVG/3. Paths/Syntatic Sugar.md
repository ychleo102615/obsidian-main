---
tags: []
date: 2026-05-14
time: 13:45
---

## Relative commands
#### 指令使用小寫：相對座標


## Horizontal / Vertical lines
`H, V` 只取用一個參數。
```css
<svg viewBox="0 0 16 16">
  <path
    d="
      M 4,4
      h 8
      v 6
    "
  />
</svg>
```

## Implied lines
```css
<svg viewBox="0 0 16 16">
  <path
    d="
      M 4,4
        12,4
        12,10
    "
  />
</svg>
```
`L` 指令可以被省略。不推薦使用。

## Chained curves
```css
<svg viewBox="0 0 16 16">
  <path
    d="
      M 4,4
      Q 4,10
        8,8
      T 12,12
    "
  />
</svg>

<svg viewBox="0 0 24 16">
  <path
    d="
      M 0,8
      C 4,0
        8,21
        12,12
      S 16,16
        24,8
    "
  />
</svg>
```

`T, S` 指令會省略第一個 control point。