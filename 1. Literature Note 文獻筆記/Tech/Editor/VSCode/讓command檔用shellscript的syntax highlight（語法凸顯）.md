---
tags: []
date: 2024-03-29
time: 14:09
---
[參考連結](https://stackoverflow.com/questions/29973619/how-to-associate-a-file-extension-with-a-certain-language-in-vs-code)

打開`setting.json`（cmd+shift+p），新增下片的片段：
```json
"files.associations": {
    "*.command": "shellscript"
},

```
