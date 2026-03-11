---
name: vocab-card-writer
description: >
  英文單字學習與 Obsidian 卡片自動建立工具。當使用者提到要學習英文單字、查字源、建立單字卡、建立字根卡、或提及 etymology / 字根字首 / flashcard / Obsidian 卡片時，使用此 skill。涵蓋：查詢單字的 etymology 並詳細解說、自動在使用者的 Obsidian vault 中建立單字卡片和字根/字首卡片、管理 wikilink 連結。即使使用者只是問一個單字的意思或字源，也應使用此 skill 以確保回答格式一致且可直接轉為卡片。
---

# Vocab Card Writer

幫助使用者學習英文單字並自動在 Obsidian vault 建立閃卡。
主要環境：Claude Code（可直接在使用者本機執行 bash + Obsidian CLI）。
Fallback：Claude.ai chat（透過 Filesystem MCP 工具）。

## 觸發時機

- 使用者問一個英文單字的意思、字源、用法
- 使用者說「幫我查 X 這個字」「X 是什麼意思」「學習 X」
- 使用者要求建立單字卡或字根卡
- 使用者提到 etymology、字根、字首、flashcard

---

## Phase 1：單字解說

1. **查詢 etymonline**：用 `web_search` 搜尋 `{word} etymology etymonline`
2. **綜合分析**：結合 etymonline 資料與模型知識，產出：
   - 中文定義（簡潔）
   - 字根字首拆解（追溯到 PIE 字根，用 `*` 標記）
   - 語意演變脈絡（字根原意 → 現代意思的邏輯鏈）
   - 意象／記憶錨點（幫助記憶的心理圖像）
   - 關聯字詞（最多 5 個，共享相同字根）
   - 例句（偏向技術或職場情境，**不附中文翻譯**）
   - 適用場景說明
3. **回覆格式**：自然段落，繁體中文，不要過度格式化。

---

## Phase 2：建立 Obsidian 卡片

回答完畢後，詢問使用者是否要建立卡片。
如果使用者同意（或一開始就要求建卡片），進入以下流程。

#### 多單字情境

若使用者一次查詢多個單字，在建立前先詢問：

> 要為每個單字建立獨立檔案，還是匯總到同一個主題檔案？

- **獨立檔案**：每個單字走標準建立流程
- **主題檔案**：詢問主題名稱（作為檔名），所有單字卡依序 append 到同一個檔案；該檔案使用 template 建立骨架（同單字卡流程 Step A–D），之後每個單字只需 append

#### 加入現有主題檔案情境

若使用者明確說「加入某個現有檔案」，或提供檔案名稱，則：
- 直接用 `obsidian append file={目標檔名}` append 卡片內容
- **不**重新建立檔案，不使用 template

### 步驟 1：讀取路徑設定

從 CLAUDE.md 中的路徑設定區塊讀取：
- `VAULT`：Obsidian vault 根目錄路徑
- `WORD_BASE`：單字卡基礎路徑（相對於 vault）
- `ROOT_BASE`：字根卡路徑（相對於 vault）
- `TEMPLATE`：單字卡 template 名稱

**路徑設定是泛用性的關鍵——不同使用者只需在 CLAUDE.md 中設定自己的路徑即可。**

### 步驟 2：確認子資料夾

單字卡需放在「年份/學習來源」子資料夾中。
- 使用者指定來源 → 使用對應名稱（如 `2026/Adv 2603`）
- 使用者未指定 → 使用 `{年份}/misc`
- 同一對話中已指定過 → 沿用，不重複詢問

### 步驟 3：檢查單字卡是否已存在

**在做任何事之前**，用 Grep tool 搜尋 vault 中是否已有該單字的閃卡：

```
Grep pattern="# {word} #card" path="${VAULT}/${WORD_BASE}"
```

- 找到 → 告知使用者「{word} 已存在（檔案：...），跳過建立」，**直接結束，不繼續後續步驟**
- 找不到 → 繼續建立流程

### 步驟 4：搜尋現有字根卡

建立檔案前，搜尋 vault 中已有的字根卡。

優先使用 Obsidian CLI：
```bash
obsidian search query="{字根關鍵字}"
```

Fallback 使用 bash：
```bash
find "${VAULT}/${ROOT_BASE}" -name "*{字根關鍵字}*" -type f
```

chat 環境使用 `Filesystem:search_files`。

記錄已存在的字根卡檔名，供 wikilink 使用。

### 步驟 4：建立單字卡

#### 寫入工具優先順序

**1. Obsidian CLI（最優先）**

⚠️ **已知限制**：`path=` 和 `name=` 參數無法處理含空格的路徑（CLI 內部解析器會截斷）。
**繞路方案**：先用純檔名（無子路徑）在 vault root 建立，再用 bash `mv` 移到目標位置，最後用 `file=` wikilink 解析 append 內容。

```bash
# Step A: 用純檔名建立（不含路徑，避免空格問題）
obsidian create name={word} 'template={TEMPLATE}'

# Step B: 驗證檔案確實建立
if [ ! -f "${VAULT}/{word}.md" ]; then
  echo "❌ obsidian create 失敗，改用 bash 寫入"
  # → 改走 bash fallback
fi

# Step C: 修正空白標題行（template 產生 `#  #card`）
sed -i '' 's/^#  #card/# {word} #card/' "${VAULT}/{word}.md"

# Step D: 移動到正確位置
mv "${VAULT}/{word}.md" "${VAULT}/${WORD_BASE}/{年份}/{來源或misc}/{word}.md"

# Step E: append 卡片內容（file= 用 wikilink 解析，自動找到移動後的檔案）
obsidian append file={word} content='{卡片內容}'
```

**注意**：
- template 含空格時需用單引號包住整個參數：`'template={TEMPLATE}'`
- `file=` 使用 wikilink 解析，不受路徑影響，可在 `mv` 後直接使用
- content 含空格時同樣需用單引號包住：`'content=...'`

**2. bash cat/echo（Obsidian CLI 不可用時）**

```bash
mkdir -p "${VAULT}/${WORD_BASE}/{年份}/{來源或misc}"

WORD_FILE="${VAULT}/${WORD_BASE}/{年份}/{來源或misc}/{word}.md"
if [ -f "$WORD_FILE" ]; then
  echo "⚠️ 已存在，跳過: $WORD_FILE"
else
  cat << 'CARD_EOF' > "$WORD_FILE"
{完整卡片內容，含 frontmatter}
CARD_EOF
  echo "✅ 已建立: $WORD_FILE"
fi
```

**3. Filesystem MCP（chat fallback）**

使用 `Filesystem:write_file` 寫入完整內容含 frontmatter。
寫入前先用 `Filesystem:search_files` 確認不存在。

#### 環境偵測

```
if `which obsidian` 成功 且 `obsidian version` 有回應:
    使用 Obsidian CLI
elif 可以執行 bash:
    使用 cat/echo
elif Filesystem:write_file MCP 可用:
    使用 MCP
else:
    產出格式化文字供手動複製
```

### 步驟 5：建立字根/字首卡片

對每個需要建卡的字根，檢查是否已存在：
- 已存在 → 跳過，使用現有檔名作為 wikilink
- 不存在 → 建立新檔案

字根卡不使用 template（內容太簡短）。

```bash
# Obsidian CLI
obsidian create \
  name="${ROOT_BASE}/{字根} \"{含義}\"" \
  content="{字根卡內容}"
```

### 步驟 6：同步到 Anki

所有卡片建立完成後，執行同步：

```bash
# 檢查 Anki 是否開啟
if ! pgrep -x "Anki" > /dev/null; then
  echo "⚠️ Anki 未開啟"
fi
```

- **Anki 未開啟** → 告知使用者，並詢問：「要開啟 Anki 並同步，還是跳過？」
  - 選擇開啟 → `open -a Anki`，等候使用者確認後繼續同步
  - 選擇跳過 → 略過，提醒之後手動同步
- **Anki 已開啟** → 直接同步：

```bash
# 切換到目標檔案（command 作用在 active file）
obsidian open 'path={WORD_BASE}/{年份}/{來源}/{word}.md'
sleep 1
obsidian command id=flashcards-obsidian:generate-flashcard-current-file
echo "✅ 已同步到 Anki：{word}"
```

**注意**：
- `obsidian open path=` 同樣有空格問題，需用單引號包住
- `sleep 1` 確保 Obsidian 切換完成後再執行指令
- 主題檔案情境：open 該主題檔案，執行一次即可同步所有卡片

### 步驟 7：回報結果

告訴使用者：
- ✅ 建立了哪些檔案
- ⏭️ 哪些字根卡已存在跳過
- ✅ / ⚠️ Anki 同步狀態
- ⚠️ 任何錯誤
- 使用了哪種寫入方式

---

## 卡片格式規範

### 單字卡

使用 Obsidian CLI + template 時，template 產生 frontmatter 和標題行骨架。
Claude 只需 append 以下內容：

```
{字根字首拆解行，用 [[字根檔名]] wikilink}  
{中文定義}  
{記憶錨點/學習情境（如有）}  
{例句（不附中文翻譯）}  
```

使用 bash 或 MCP 時，需寫入完整內容含 frontmatter。**date 和 time 必須用 bash 動態取得**：

```bash
CARD_DATE=$(date "+%Y-%m-%d")
CARD_TIME=$(date "+%H:%M")
```

然後寫入：
```
---
tags:
  - flash-cards
  - Engslish-flash-card
date: {CARD_DATE}
time: {CARD_TIME}
cards-deck: 英文
---

# {word} #card  
{字根字首拆解行}  
{中文定義}  
{記憶錨點/學習情境（如有）}  
{例句（不附中文翻譯）}  
```

**格式要點**：
- `# {word} #card` 行尾 → 兩個 trailing spaces
- 每行內容行尾 → 兩個 trailing spaces
- frontmatter 行 → 不加 trailing spaces
- `Engslish-flash-card` → 保持此拼法
- **不重複列出 PIE 字根**——wikilink 已涵蓋的字根資訊不另外文字重述
- 例句不附中文翻譯

**字根拆解規則**：
- 可追溯的字根 → `[[字根檔名]]` wikilink
- 不可考字根 → 直接原文描述，如 `-ert(技能、活力，源自拉丁文 ars)`

### 字根卡

**檔名**：`{字根} "{簡短英文含義}"`（不含 `.md`）
- PIE 字根帶 `*` 前綴
- 含義從 etymonline 截取，保持簡短

**內容**（簡潔，一到兩行）：
```
{etymonline 簡短描述} (see [{字根}]({etymonline_url}))
```
或：
```
{etymonline_url}
```

---

## 重要原則

1. **事實檢查**：etymology 必須基於 etymonline 查詢結果。無資料時標註「這是推論」。
2. **Wikilink 精確匹配**：`[[檔名]]` 必須與實際字根卡檔名完全一致。
3. **不覆蓋現有檔案**：任何方式都先檢查是否存在。
4. **風格一致**：與 vault 中現有卡片保持一致。
5. **不可考字根**：保留原文描述，不強建字根卡。
6. **不重複資訊**：wikilink 已涵蓋的不另外重述。
