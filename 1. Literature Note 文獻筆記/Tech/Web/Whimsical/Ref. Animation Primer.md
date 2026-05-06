---
tags: []
date: 2026-05-06
time: 22:05
---



# Fill Modes
使用 CSS keyframes 動畫時，動畫最終的狀態可能會與我們初始設定的狀態不一樣。
例如預設 `opacity: 1`，但是動畫演出完畢時應該要 `opacity: 0` 才比較自然。
此時可以使用：
```css
{
	animation: forwards;
	/* or */
	animation-fill-mode: forwards;
}
```

其他還有 `backwards`, `both`。

但是這有缺點，keyframes 的優先度很高，這會導致其他 CSS 操作設定都被 keyframes 覆寫。