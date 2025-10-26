---
tags: []
date: 2025-10-24
time: 00:17
---

這樣寫：

```ts
import HomePage from '@/views/HomePage.vue'  
export default [   
	{ path: '/', name: 'home', component: HomePage }
]
```

這時候 **Webpack / Vite** 在建置時，會把整個 `HomePage.vue` 的程式碼  
**打包進主 bundle（例如 app.js）** 裡面。

- 首次載入網站時（例如進入首頁前），瀏覽器會先下載 **整個應用的所有頁面代碼**。
- 無論使用者是否會去 `/about`、`/profile` 頁面，那些頁面的代碼也都會被下載。
- 造成 **初始載入時間（Time to Interactive）變長**。


```ts
{
	path: '/',
	name: 'home',
	component: () => import('@/views/HomePage.vue'),
}
```

這裡的 `import()` 是 **動態匯入 (dynamic import)**，是 ES2020 的語法。  
Webpack / Vite 會自動幫你做 **code splitting（程式碼分割）**：
- `HomePage.vue` 會被打包成一個獨立的 chunk（例如：`HomePage.[hash].js`）
- 只有當使用者真的「進入該路由」時，這個 chunk 才會被載入。


### ⚙️ 實際執行流程

1. 使用者打開首頁 `/`  
    → Vue Router 執行 `component: () => import('@/views/HomePage.vue')`  
    → 瀏覽器發送一個額外的請求下載這個 chunk（lazy load）。
    
2. Vue 解析完畢後才掛載該元件。
    
3. 如果使用者從首頁跳轉到 `/about`，  
    這時才會再去載入 `AboutPage.vue` 對應的 chunk。