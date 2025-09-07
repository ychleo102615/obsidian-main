---
tags: []
date: 2025-09-06
time: 20:45
link: https://blog.poychang.net/obsidian-sync-between-desktop-and-mobile-with-git/
---
### 1. 初始化git

### 2. 安裝 Obsidian Git
遇到一個問題，因為本來放在iCloud的關係，背景自動更動還是怎樣的時候，會改到git。
所以有一陣子他顯示所有檔案都被刪除，而且頂部資料夾處在沒有追蹤的狀態。

### 3. 在iPhone上使用iSH，讓git可以工作
參考上面的link。
踩到幾個坑：
1. iSH mount外部資料夾的時候，要先建好該資料夾
2. git personal access token 要注意有寫入權限（在content那裡要打勾）
3. 後來在iPad上用也卡了一下，處理merge衝突。這個同步方式恐怕一次最好只用一個裝置來編輯吧。
4. 建立每日筆記容易衝突