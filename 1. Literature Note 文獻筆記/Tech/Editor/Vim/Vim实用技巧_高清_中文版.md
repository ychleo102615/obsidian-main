---
tags: vim
date: 2023-04-19-週三
time: 12:31
---

[ebook](https://github.com/lijasonvip/Books_Reading/blob/master/Vim%E5%AE%9E%E7%94%A8%E6%8A%80%E5%B7%A7_%E9%AB%98%E6%B8%85_%E4%B8%AD%E6%96%87%E7%89%88.pdf)

### 技巧 99 将 TODO 项收集至寄存器
1. run `qaq` 清空暫存器 a
2. run `:g/your_pattern/yank A`

首先要清空暫存器。然後yank A 使用大寫代表你不會把目前暫存器裡面的值清空，才能將整份文件中符合的行累積下來。