---
tags: []
date: 2025-05-18
time: 14:17
---

> [!NOTE]
> ### Requirement
> Excellent skills in Java, Scala, Python, or Go 
> Strong fundamentals in data structures, algorithms and object oriented programming 
> Experience with microservices and designing high traffic systems 
> 
> ### Process
> Coding Test 
> 1st Interview 
> 2nd Interview (Loop Interview)
> 	Programming, Data Structure and Algorithm 
> 	Software Design and Architecture 
> Final Interview

| 時段           | 任務類型                                      | 說明                               |
| ------------ | ----------------------------------------- | -------------------------------- |
| 5月下旬～6月中旬    | 完成 DDIA + 持續刷題                            | 建議每天輪流切換：一日 DDIA + 一日 NeetCode   |
| 6月下旬～7月      | 開始 System Design Interview 閱讀 + 實作第 1 個專案 | 輕量專案先做起，有成果最重要                   |
| 8月～9月        | 完成專案、熟練系統設計口語化描述                          | 嘗試用英文講解每個專案設計理念                  |
| 9月中～10月      | 使用 Hello Interview 模擬練習                   | 記錄弱點、加強口語表達                      |
| 10月中～11月<br> | 投遞履歷與 mock interview                      | 可使用 Pramp、Interviewing.io 模擬口語演練 |

# 📚 學習內容建議與調整
### 1. **DDIA 後期閱讀建議**
- 第 9～12 章偏向專業資料處理領域（batch, stream processing, 分析系統等），雖然對「基礎功」非常有幫助，但不一定在面試中直接出現。
- 建議：**閱讀時快速抓主線與核心概念（例如事件時間 vs 處理時間、exactly-once semantics、stream-table duality）即可**，不用死磕太細節。

### 2. **System Design Interview 書的閱讀安排**
- 書中內容多半是短篇範例導向，可以安排為每天/隔天讀一題，邊讀邊手繪架構圖與重述設計選擇原因。
- 建議讀書順序：
    1. Rate Limiter
    2. URL Shortener
    3. Message Queue
    4. Notification System
    5. Web Crawler / Search Engine

### 3. **NeetCode 150**
- 每天一小時非常理想。若遇到困難題，可以用「三日節奏」：第一天建模與初解，第二天優化，第三天重寫 + 回顧同類題（類題串連式學習法）。

### 4. **Hello Interview 使用建議**
- 這類網站的「系統設計模擬面試」與「behavioral question」非常實用，但建議等到你能口語完整描述系統設計題目的程度再開始使用，效果最佳。
- 配合使用方式：**模擬回答後錄音回放 → 檢查邏輯與語言表達 → 用英文重寫並背誦模範解答。**


## 💼 實務經驗與作品安排
你提到想在這段期間累積實務經驗（7 成後端 / 3 成前端），這是很明智的補強策略，尤其對轉職很加分。建議如下：
### 可行途徑
1. **打造個人專案**（推薦優先）
    - 小型 SaaS 系統（ToDo, Expense Tracker, Trading Dashboard）
    - 重點：使用後端技術 + 登入系統 + RESTful API + DB 設計 + 部署（Heroku, Render, Vercel 都可）
2. **貢獻 Open Source（如 GitHub issues, Docs）**
    - 貢獻類型：小修 bug、翻譯文檔、加測試、寫 README。
    - 可加分項：如果你會 TypeScript/Lua，找有興趣的遊戲框架或工具加入也很棒。
3. **Freelance / Intern / Pro Bono 企劃**
    - 上 Upwork 或接身邊朋友 side project
    - 可以是網站重構、API 設計等，用實例補強你在履歷上的項目數量。
### 技術堆疊建議（後端）
- Python + FastAPI / Node.js + Express / NestJS
- PostgreSQL / Redis
- Git + CI/CD + Docker（加分）
- 部署至 Railway / Render / AWS Free Tier