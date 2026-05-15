---
tags: []
date: 2026-05-15
time: 14:15
link: https://courses.joshwcomeau.com/wham/02-svg/08.05-non-bezier-exercises
---
## Toast notifications

除了動畫本，要注意的有兩個：

一、使用 CSS 變數 fallback 舊瀏覽器
```css
.toast {
    /*
    For folks on older browsers, a Bézier curve will be used
    as a fallback. This curve mimics a spring, overshooting the
    target and then settling back.
    */
    --spring-easing: cubic-bezier(0.154, 1.937, 0.213, 0.901);
    --spring-duration: 1.167s;
    --inset-by: 16px;
    ...
    
}
@supports (transition: linear(0, 1)) {
    .toast {
        --spring-easing: linear(...);
    }
}
```


二、減少動畫特效
```css
@media (prefers-reduced-motion: no-preference) {
    /* On enter, use the spring defined above. */
    .toast {
    transition:
        transform var(--spring-easing) var(--spring-duration);
    }
    /*
    On exit, use an “ease-in” style curve.
    This prevents the weird oscillation flicker that occurs
    with a spring,
    */
    .toast.hidden {
        transition:
            transform cubic-bezier(0.598, 0.029, 0.876, 0.573) 200ms;
    }
}
```


我用了巢狀做法，雖然有效，但是有 bug。