---
tags: []
date: 2026-05-14
time: 12:23
---

## Move
`M`
```css
<path d="M 10,10" />
```

**Every path command we write _must_ start with a Move command.**

## Line
`L`

## Closing paths
`Z`
```css
<svg viewBox="0 0 16 16">
  <path
    d="
      M 4,4
      L 4,12
      L 12,12
      Z
    "
  />
</svg>
```

回到第一個點

## Bézier curves

#### Quadratic  Bézier curves
可以使用一個控制點。
```css
<svg viewBox="0 0 16 16">
  <path
    d="
      M 2,2
      Q 2,15
        14,14
    "
  />
</svg>
```

#### Cubic Bézier curves
可以使用兩個控制點。

```css
<svg viewBox="0 0 16 16">
  <path
    d="
      M 2,2
      C 2,14
        14,2

        14,14

    "

  />

</svg>
```