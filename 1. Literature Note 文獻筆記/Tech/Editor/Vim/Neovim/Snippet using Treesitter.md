---
tags: neovim
date: 2023-04-20-週四
time: 13:05
---

## Example:  Automatically add quotes in Vue element attributes
[來源](https://medium.com/scoro-engineering/5-smart-mini-snippets-for-making-text-editing-more-fun-in-neovim-b55ffb96325a)

```lua
--ftplugin/vue.lua  
vim.keymap.set('i', '=', function()  
	-- The cursor location does not give us the correct node in this case, so we  
	-- need to get the node to the left of the cursor  
	local cursor = vim.api.nvim_win_get_cursor(0)  
	local left_of_cursor_range = { cursor[1] - 1, cursor[2] - 1 }  
	  
	local node = vim.treesitter.get_node { pos = left_of_cursor_range }  
	local nodes_active_in = {  
	'attribute_name',  
	'directive_argument',  
	'directive_name',  
	}  
	if not node or not vim.tbl_contains(nodes_active_in, node:type()) then  
	-- The cursor is not on an attribute node  
	return '='  
	end  
	  
	return '=""<left>'  
end, { expr = true, buffer = true })
```