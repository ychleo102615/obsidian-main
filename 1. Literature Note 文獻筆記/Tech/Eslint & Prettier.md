先跳過如何安裝（vue已有工具協助建立）


# 更改縮排長度
## 1. 設定prettier
```
// .prettierrc.json
{
    "tabWidth": 4
}

```
[參考](https://prettier.io/docs/en/configuration.html)

## 2. 在eslint 中加入prettier
```
// .eslintrc.cjs
module.exports = {
    ...
    extends: [
        ...
        "prettier",
    ],
}
```

## 其他
nvim null_ls 遇到 eslint_d 是有問題的
[參考](https://www.reddit.com/r/neovim/comments/uhgwyh/nullls_eslint_formatter_doesnt_pick_up_project/)
editor config https://editorconfig.org/
[參考](https://prettier.io/docs/en/configuration.html#editorconfig)
