---
tags: []
date: 2026-05-07
time: 14:23
link: https://courses.joshwcomeau.com/wham/animation-primer/02-transform-functions
---
# Translation
```css
transform: translateX(calc(0% + 0px));
```

百分比會應用在自分的尺寸上。


# inline elements
transform 無效。
可以加上 `display: inline-block`修正。
或者是應用在 Flexbox or Grid 之下。


> [!NOTE] A different mechanism
> 
> 
> This reveals an important truth about transforms: **elements are flattened into a texture**. All of these transforms essentially treat our element like a flat image, warping and contorting it the same way you would in graphic-editing software like Photoshop.
> 
> This allows the browser to “re-use” any work that has previously completed. When we change a `transform` property, the browser doesn't have to recalculate the layout, or re-run the line-wrapping algorithm, or handle rasterization. Transforms are super efficient, which is part of why they’re such a great choice for animation!

