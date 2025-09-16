---
tags: [devnote]
date: 2025-09-16
time: 23:11
layout: doc
---

# Claude

<DocDate :date="$frontmatter.date" />

以下是我在Claude打的提示詞：

> [!NOTE]
> 幫我建立一個claude code使用的.CLAUDE.md 檔案。 我想要使用vue3來製作一個日本花牌遊戲：來來。 
> - 技術方面：vue專案要使用typescript，css使用tailwind。 
> - 架構：嚴格幫我指名我要使用clean architecture來實作。 
> - UI：在這個框架下，其中一個特色是，遊戲介面我不只可以使用html普通文流來實作，而是我未來想要轉成利用pixi.js或是其他webGL框架來建立更完整的遊戲都可以。所以也就是在clean architecture中，我可以有兩種UI細節，隨我喜歡的切換。 
> - 核心邏輯：目前遊戲邏輯打算在typescript寫，但是未來也要切換成用api與server溝通，這些功能都因為有clean architecture而有乾淨的界線。所以注意，一開始專案中應該就要有兩個領域，一個是遊戲規則領域，一個是前端領域。遊戲規則領域是可以在切換成server時被擱置的（甚至變成離線遊戲的功能）。

接下來是要課金的部分了。


遇到的錯誤：Tailwind他預設安裝v3，目前好像都是使用v4。

跑到中途我有了一個疑問，我是不是應該先用計劃模式設計好，再請他實作？

之前的教學有提到playright，我這次沒先連接起來。

我是先在Claude上面設計的（沒花錢），而code是依照該設計實踐的。會不會讓code自己設計，得到結果會更好？



> [!claude]
>  完成！我已經成功按照 CLAUDE.md 中的規劃開發了日本花牌遊戲專案。
> 
>   專案完成總結
> 
>   ✅ 設置 Vue 3 + TypeScript + Tailwind 專案基礎配置 - 完成 Vite + Vue 3 + TypeScript 配置，整合 Tailwind CSS v4
>   ✅ 建立 Clean Architecture 目錄結構 - 建立完整的分層架構目錄
>   ✅ 實現 Domain Layer 核心實體 - 完成 Card、Player、GameState、Yaku 實體
>   ✅ 建立 Domain Layer 介面定義 - 完成 GameRepository 和 UIRenderer 介面
>   ✅ 實現基本的 Use Cases - 完成 PlayCard、CalculateScore、GameFlow Use Cases✅ 建立 Infrastructure Layer 的 LocalGameRepository - 完成本地遊戲邏輯實現
>   ✅ 實現 HTML DOM 版本的基礎 UI 元件 - 完成 CardComponent、PlayerHand、GameBoard、GameView
>   ✅ 測試專案基本功能 - 通過 TypeScript 類型檢查、ESLint 檢查和生產構建
> 
>   專案特色
> 
>   1. Clean Architecture 設計 - 嚴格的分層架構，領域邏輯與 UI 完全分離
>   2. 類型安全 - 完整的 TypeScript 類型定義和檢查
>   3. 可擴展性 - 支援未來擴展 WebGL 渲染器和遠端 API
>   4. 遊戲功能完整 - 實現完整的花牌遊戲邏輯、役種判定和計分系統

燒了$4.3。成果差強人意：

# TODO
1. 讓遊戲可以走完
2. 調整網站整體layout
3. 看懂程式碼

[連結](https://github.com/ychleo102615/hanahuda)
