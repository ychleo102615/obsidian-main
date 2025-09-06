---
tags: []
date: 2024-01-10-週三
time: 14:50
---

> [!NOTE] chat-gpt
>tolua++ 是一個工具，用於將 C/C++ 代碼整合到 Lua 中。它是 tolua 工具的升級版本，允許開發人員更輕鬆地將 C/C++ 函數、類和物件導出到 Lua 中，以便在 Lua 腳本中直接使用這些函數和物件。
>
>tolua++ 提供了一種自動化的方式來生成綁定代碼，將 C/C++ 中的函數、類和物件映射到 Lua 腳本中。這種綁定允許開發人員在 Lua 中調用 C/C++ 的功能，從而實現兩種語言的交互操作。這對於遊戲開發、嵌入式系統以及需要在不同語言間進行交互的項目非常有用。

# [tolua++中文参考手册](https://github.com/dabing1022/Blog/blob/master/tolua/tolua%2B%2B中文参考手册%5B完整翻译%5D.md#tolua中文参考手册完整翻译)


```
传给tolua的package文件并不是真正的C/C++头文件，而是清理过的版本。
```

```shell
./tolua++ -L basic.lua -o ../../scripting/lua/cocos2dx_support/LuaCocos2d.cpp Cocos2d.pkg

```

- `-L basic.lua` 指定了一些hook，在運行tolua++的時候可以呼叫到
- `-o` 指定了輸出檔名
- `Cocos2d.pkg` 即是產生綁定程式碼的參考來源