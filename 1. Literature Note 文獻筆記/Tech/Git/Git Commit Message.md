---
tags: []
date: 2024-12-25
time: 14:09
---
[Git Commit Message 這樣寫會更好，替專案引入規範](https://wadehuanglearning.blogspot.com/2019/05/commit-commit-commit-why-what-commit.html)
https://www.conventionalcommits.org/en/v1.0.0/

### type 只允許使用以下類別：

| title     | meaning                                                             |
| --------- | ------------------------------------------------------------------- |
| feat:     | 新增/修改功能 (feature)。                                                  |
| fix:      | 修補 bug (bug fix)。                                                   |
| docs:     | 文件 (documentation)。                                                 |
| style:    | 格式 (不影響程式碼運行的變動 white-space, formatting, missing semi colons, etc)。 |
| refactor: | 重構 (既不是新增功能，也不是修補 bug 的程式碼變動)。                                      |
| perf:     | 改善效能 (A code change that improves performance)。                     |
| test:     | 增加測試 (when adding missing tests)。                                   |
| chore:    | 建構程序或輔助工具的變動 (maintain)。                                            |
| revert:   | 撤銷回覆先前的 commit 例如：revert: type(scope): subject (回覆版本：xxxx)。         |

---
### chatgpt

#### ✅ 常見的 chore 用途
	1.	專案設定與維護
	•	chore: update dependencies（更新依賴）
	•	chore: update ESLint config（更新 ESLint 設定）
	•	chore: configure CI/CD pipeline（設定 CI/CD 流程）
	2.	檔案或專案結構的調整（不影響功能）
	•	chore: move utils to separate folder（將工具函式移動到獨立的資料夾）
	•	chore: rename files for consistency（重新命名檔案以保持一致性）
	3.	格式化與程式碼整理（無行為變更）
	•	chore: format code with Prettier（用 Prettier 格式化程式碼）
	•	chore: rearrange imports（重新整理 import 順序）
	•	chore: remove unused variables（移除未使用的變數）](chore:)

關鍵點是**有沒有影響功能**：
• ✅ **不影響功能 = chore**
• ✅ **程式碼結構優化 = refactor**
• ✅ **效能優化 = perf**

#### 刪除功能
• ✅ **刪除舊功能、清理不必要的程式碼** → refactor
• ✅ **刪除已棄用的功能、非必要的維護** → chore
• ✅ **刪除功能是產品決策的一部分（例如移除某個按鈕）** → feat
• ✅ **刪除某段程式碼是為了修復 bug** → fix
