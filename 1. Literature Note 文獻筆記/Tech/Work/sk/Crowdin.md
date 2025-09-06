---
tags: 
date: 2023-10-11-週三
time: 15:11
---
# [crowdin](https://crowdin.com/)
管理專案文本、資源檔案的翻譯工作的平台。用起來有點像github的雲端託管平台。


> [!NOTE]-
> 目前公司帳號上的專案的使用情況，是建立csv檔案對應許多字串。美術檔案還沒傳上去的樣子。

## 如何使用CLI
[官方文件](https://crowdin.github.io/crowdin-cli/)

1. `brew install crowdin`安裝
2. 建立好帳號以及專案
3. 使用指令`crowdin init`，會在當前資料夾初始化專案。完成後會新增`crowdin.yml`檔案。
4. 按照專案需求調整`crowdin.yml`這個config檔案。請參考[這裡](https://developer.crowdin.com/configuration-file/)。
5. 之後就可以上傳、下載了。`crowdin upload`、`crowdin download`

CLI token 每30天會過期，需要定期更新。


## Config檔案
我自己先在遠端建立，再使用CLI下載，會出現檔案結構不一致的問題。先從本地上傳的話，這個問題就解決了。
config檔案有幾個元素：
- `source`: 原版檔案格式
- `translation`: 翻譯版本的檔案位置

## 檔案結構
在我們使用crowdin upload之前，需要先在config檔案中寫好`source`和`translation`的指定檔案位置。這樣子第一次上傳時，**每個檔案都會被設定它之後被下載的位置**。否則手動調整會太繁瑣。
每個檔案的下載位置，可以在`Sources`籤頁上，點檔案最右邊的設定按鈕，檢查檔案的下載位置（注意這邊可以與上傳的檔案結構位置不一樣）。

- 若是下載位置與`translation`指定格式不同的話，會下載失敗。
- 先下載`sources`：`crowdin pull sources`
- 如果本地端沒有source files的話，可以用`crowdin pull --all`。
- `crowdin upload --no-auto-update` 可以略過已上傳的檔案（否則會再上傳一次）


這樣的組合可以有多組：
```yaml
"files": [
  {
      "source": "/**/?[0-9].txt", #upload a1.txt, folder/a1.txt
      "translation": "/**/%two_letters_code%_%original_file_name%"
  },
  {
      "source": "/**/*\\?*.txt",  #upload crowdin?test.txt, folder/crowdin?test.txt
      "translation": "/**/%two_letters_code%_%original_file_name%"
  },
  {
      "source": "/**/[^0-2].txt", #upload 3.txt, folder/3.txt, a.txt, folder/a.txt (ignore 1.txt, folder/1.txt)
      "translation": "/**/%two_letters_code%_%original_file_name%"
  }
]

```

#### [Asset Localization](https://support.crowdin.com/assets-localization/#typical-asset-references)

## String
在網站介面，Sources籤頁有`Files`和`Strings`。前者是我們上傳的檔案；後者是我們上傳的檔案中，例如有csv檔案的話，它可以把裡面的資訊「匯入」。
## bundle
這是將Strings打包下載的功能。


## 跳過的部分
我認為我們用不到的部分：
1. glossaary（定義專有詞彙，可能只會有企劃用）
2. translation memory (簡稱tm，加速大型專案翻譯用)
3. distribution  (有關cdn發布的功能)

