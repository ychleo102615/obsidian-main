---
tags: []
date: 2025-07-29
time: 23:43
---
`vite.config.js`檔案中，可以指定`base`。

```js
export default defineConfig({
  base: '/Server/',
  plugins: [
    vue(),
    vueDevTools(),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    },
  },
})

```


`base` 是為了部署時能對應到正確路徑，而開發時 Vite dev server 會幫你把路徑處理得很好，所以「開發不會出錯，但部署要小心 base 的正確性」。



## ✅ 實戰建議

若你要部署到 GitHub Pages，repo 叫做 `vite-2025-practice`，就這樣設定：

```js
export default defineConfig({
  base: '/vite-2025-practice/',
})

```