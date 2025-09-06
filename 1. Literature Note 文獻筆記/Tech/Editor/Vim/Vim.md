## c-r c-w 命令模式插入游標單字
[連結](https://zhuanlan.zhihu.com/p/82676724)

## 生成遞增數字
 [連結](https://irian.to/blogs/quick-vim-tips-to-generate-and-increment-numbers/)

```vimscript
:put=range(1,5)
``` 

對已列出的數字遞增
1. 選取範圍
2. g ctrl-a

---
[[2023-04-27]]
```vim
:'<,'>s/\s*$/,
取代範圍內每行尾部的空白

```

---
[[2023-07-03|2023-07-03-週一, 18:00]]
## 刪除所有Buffers
```vimscript
:%bd
```
[參考來源](https://www.reddit.com/r/vim/comments/8d4dee/how_do_i_close_all_files_but_not_quit_vim/)

---
[[2023-07-31|2023-07-31-週一, 10:54]]
## [[全域搜尋取代的替代方案]]

---
[[2023-08-24|2023-08-24-週四, 17:22]]
## 在新標籤頁開啟當前Buffer
`:tab sp`

輸入 `:h :tab`  來開啟vim的說明

[來源](https://superuser.com/questions/66179/how-do-i-edit-an-existing-buffer-in-a-new-tab-in-vim)


[[2024-01-23|2024-01-23, 16:24]]
## 刪除不符合特定格式的行
[參考](https://superuser.com/questions/265085/how-to-delete-all-lines-that-do-not-contain-a-certain-word-in-vim)
```vim
:g /price/d
:g!/price/d
:v/price/d
```

[[2024-10-23|2024-10-23, 09:46]]
## 取消空白對齊
```vim
:s/\s\+/ /g
```
但是這會連同第一個縮排一起調整