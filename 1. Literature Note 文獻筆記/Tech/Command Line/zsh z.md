---
tags: []
date: 2024-01-30
time: 22:34
---
[link](https://github.com/agkozak/zsh-z)
[[2024-01-25#Note]]
我在公司的電腦有裝zsh-z，後來在家裡的電腦同樣這樣裝，卻沒有成功。

今天參考git上面的安裝指示，倒是一下就裝好了。


> [!NOTE] zsh-z 
>
>### General observations
>
>This plugin can be installed simply by putting the various files in a directory together and by sourcing `zsh-z.plugin.zsh` in your `.zshrc`:
>
>```
>source /path/to/zsh-z.plugin.zsh
>```
>
>For tab completion to work, `_zshz` _must_ be in the same directory as `zsh-z.plugin.zsh`, and you will want to have loaded `compinit`. The frameworks handle this themselves. If you are not using a framework, put
>
>```
>autoload -U compinit; compinit
>```
>
>in your .zshrc somewhere below where you source `zsh-z.plugin.zsh`.
