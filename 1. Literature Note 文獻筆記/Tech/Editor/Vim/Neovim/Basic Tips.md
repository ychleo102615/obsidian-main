[初始化教學](https://www.youtube.com/watch?v=stqUbv-5u2s)
[初始化腳本連結](https://github.com/nvim-lua/kickstart.nvim)

# Lsp

## lua-language-server

[自行載入library](https://github.com/LuaLS/lua-language-server/wiki/Annotations)
這需要尋找一下lsp server library的位置，就lua-language-server而言在這裡(mason)： [loc](~/.local/share/nvim/mason/packages/lua-language-server/extension/server/meta/3rd/)
之後需要在專案建立`.luarc.json`檔案
```
{
    "runtime.version": "LuaJIT",
	"runtime.path": ["/src/?.lua"],
	"workspace.library": [
	    "${3rd}/Cocos2dx/library"
    ],
    "workspace.checkThirdParty": false,
    "diagnostics.globals": [
	    "class", "clone", "Toast"
    ]
}
```



## Passing a count to a user command with neovim's Lua API
[來源](https://vi.stackexchange.com/questions/38352/passing-a-count-to-a-user-command-with-neovims-lua-api)
```lua
vim.v.count
map("n", "<leader>m", function()
    vim.cmd("tabnext " .. (vim.v.count == 0 and "" or vim.v.count));
end, { desc = "Next Tab With Number" })

```


## Lazy Events
載入plugins時可以參考的events
原生event: [[Events]]
[User Events](https://github.com/folke/lazy.nvim#-user-events)
Vim Events:
```
:help autocmd-events
```