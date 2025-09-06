在為nvim加入java lsp時，發現連[nvim-lspconfig](https://github.com/neovim/nvim-lspconfig/blob/master/doc/server_configurations.md#jdtls)本身，都推薦使用[nvim-jdtls](https://github.com/mfussenegger/nvim-jdtls)，因為後者提供更全面的功能，如`extract_method`等。

有幾個比較重要的安裝步驟，我想記錄一下：

## 1. eclipse.jtd.ls 下載
去此處下載jdtls：[網址](https://github.com/eclipse/eclipse.jdt.ls#installation)
雖然網站說是安裝，但其實也只是下載這個壓縮檔而已。

## 2. 安裝 java 17
jtd需要安裝java 17以上，我是用了brew install java來裝的，那這個版本在安裝完的訊息有提示你他的位置：
```
==> Summary
🍺  /usr/local/Cellar/openjdk/19.0.2: 636 files, 318.7MB
```
這個位置在跑jtdls時會用到。

其他也有看到網路上其他人的建議：[參考](https://stackoverflow.com/questions/69875335/macos-how-to-install-java-17)
