---
tags: 
date: 2023-06-23-週五
time: 15:42
---

```
touch .gitignore

git rm --cached the_file_to_ignore
```
因為我發現加了.gitignore沒反應，查了一下發現，在ignore檔生成前就存在的檔案，已經算是在追蹤的檔案了，需要再手動移除掉它。

[來源](https://gitbook.tw/chapters/using-git/ignore)
