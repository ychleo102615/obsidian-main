---
tags: []
date: 2025-09-07
time: 13:48
---

我想為個人專案做一個開發筆記記錄。
昨天問了gpt之後，他給我幾個工具：`Hugo`, `Jekyll`, `VitePress`。

雖然視覺上`Jekyll`看起來挺讚的（以前看過很多類似網站是用這個工具），
但因為我個人常用`Obsidian`作筆記，而VitePress能夠直接md檔案換成vue頁面，也更方便用vue工具做其他應用，就選VitePress了。

### Obsidian使用Git同步
本來我都是用iCloud同步，為了幾個原因改成用Git同步：
1. 方便同步Obsidian到VitePress這邊，想到可以用submoudle, subtree的方式來管理。但現在棄用這個方式了。
2. iPhone, iCloud行動裝置同步常常出問題，裝置因為iCloud原因會優化空間刪減，所以平常大部分的時間都沒法在裝置上面用。

### 使用rsync同步Obsidian資料夾到VitePress專案
本來用submodule, subtree的。但是實際操作起來太費工了，用rsync的話只要發部或是測試的時候跑一次就OK了。

參考[[使用Github 同步]]

