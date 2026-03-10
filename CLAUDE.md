# Obsidian Vault - Claude Code 設定

此專案是一個 Obsidian vault，主要用於知識管理和語言學習。

## 路徑設定（vocab-card-writer skill 使用）

```
VAULT=/Users/leo-huang/LocalDocuments/Obsidian/Main
WORD_BASE=6. Flash Cards/English
ROOT_BASE=6. Flash Cards/English/archived/root
TEMPLATE=4. English flash card
```

## Skills

- `.claude/skills/vocab-card-writer/SKILL.md`：英文單字學習與 Obsidian 卡片自動建立工具

## 注意事項

- 使用 Obsidian CLI（v1.12+）操作 vault，優先於直接寫檔
- 單字卡使用 template `4. English flash card` 建立
- 字根卡放在 `6. Flash Cards/English/archived/root/`
- 單字卡按年份和學習來源分子資料夾，未指定來源時用 `misc`
- 所有回覆使用繁體中文
