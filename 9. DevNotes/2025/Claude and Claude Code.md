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