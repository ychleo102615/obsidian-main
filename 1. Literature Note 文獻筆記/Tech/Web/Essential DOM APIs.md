---
tags: []
date: 2026-02-26
time: 12:14
---
# Essential DOM APIs（框架時代仍必須熟悉的原生 API）

> [!tip] 核心觀念 框架管的是「UI 隨資料變化而更新」，但**焦點、滾動、測量、全域事件、瀏覽器原生功能**這些不在資料流裡的東西，永遠需要直接和 DOM 打交道。

---

## 1. 焦點管理

```ts
element.focus()
element.blur()
document.activeElement
```

- 框架的宣告式渲染管不了「焦點現在在哪」
- 場景：Focus Trap（Modal）、表單驗證後聚焦錯誤欄位

> [!info] 相關筆記 [[Focus Trap]]、[[tabindex]]

---

## 2. 選取與剪貼簿

```ts
document.getSelection()
navigator.clipboard.writeText(text)
navigator.clipboard.readText()
```

- 場景：「複製連結」、「複製程式碼」按鈕

---

## 3. 滾動控制

```ts
element.scrollIntoView({ behavior: 'smooth' })
element.scrollTo()
window.scrollY
```

- 場景：錨點定位、無限滾動、「回到頂部」、聊天室自動滾到最新訊息

---

## 4. 尺寸與位置測量

```ts
element.getBoundingClientRect()
window.innerWidth / innerHeight
```

- 場景：tooltip 定位、拖曳邊界計算、判斷元素是否在可視範圍內

---

## 5. 事件監聽（框架外的對象）

```ts
window.addEventListener('resize', handler)
window.addEventListener('popstate', handler)
document.addEventListener('keydown', handler)
document.addEventListener('visibilitychange', handler)
```

- 框架的事件綁定只管得到它自己渲染的元素
- `window`、`document` 層級的全域事件需要自己掛
- 場景：快捷鍵、視窗縮放、頁面可見性變化

---

## 6. Observer 系列

```ts
new IntersectionObserver(callback)  // 元素進出視窗
new ResizeObserver(callback)        // 元素尺寸變化
new MutationObserver(callback)      // DOM 結構變化
```

|Observer|用途|
|---|---|
|`IntersectionObserver`|懶載入圖片、無限滾動|
|`ResizeObserver`|響應式元件、容器查詢|
|`MutationObserver`|偵測第三方 DOM 改動|

- 通常包在 custom hook（React）/ composable（Vue）裡面使用

---

## 7. `<dialog>` 相關

```ts
dialog.showModal()
dialog.close()
```

- 目前做 Modal 最正確的方式
- 框架只幫你拿到 ref，開關還是要呼叫原生 API
- `showModal()` 自動建立 focus trap、背景 `inert`、Esc 關閉

---

## 8. 類別與屬性操作

```ts
element.classList.add(cls)
element.classList.remove(cls)
element.classList.toggle(cls)
element.classList.contains(cls)

element.setAttribute(name, value)
element.getAttribute(name)
element.dataset  // data-* 屬性
```

- 框架通常用綁定處理，但和第三方函式庫或動畫庫互動時仍會直接操作

---

## 9. requestAnimationFrame

```ts
requestAnimationFrame(callback)
```

- 場景：自訂動畫、Canvas 繪製、高效能的拖曳或滾動效果

---

## 10. History API

```ts
history.pushState(state, '', url)
history.replaceState(state, '', url)
```

- React Router / Vue Router 底層就是包裝這個
- 理解底層才能除錯路由問題，也能在需要時繞過框架直接操作

---

## 11. querySelectorAll

```ts
document.querySelectorAll('button:not(:disabled)')
element.querySelectorAll('[tabindex]:not([tabindex="-1"])')
```

- 接受的參數就是 CSS 選擇器字串，和 `.css` 裡寫的語法完全一樣
- 場景：Focus Trap 中收集可聚焦元素、與第三方 DOM 互動