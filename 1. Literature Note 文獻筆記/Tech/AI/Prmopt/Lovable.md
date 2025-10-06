---
tags: []
date: 2025-10-06
time: 13:13
link: https://docs.lovable.dev/prompting/prompting-one?fbclid=IwY2xjawNQKedleHRuA2FlbQIxMQABHlQa3WBfBTGaAH4D_6MUJ8Z_hpNuMpB_GB3if5adavPBpTkPEPJWShQ6AItM_aem_hFBrUFLh8-p9a8Y9dgyR7g
---



- **Context:** Background or role setup for the AI. (E.g. “You are a world-class Lovable AI coding assistant.”)
- **Task:** The specific goal you want to achieve. (E.g. “Build a full-stack to-do list app with user login and real-time sync.”)
- **Guidelines:** Preferred approach or style. (E.g. “Use React for frontend, Tailwind for styling, and Supabase for auth and database.”)
- **Constraints:** Hard limits or must-not-dos. (E.g. “Do not use any paid APIs. The app should work on mobile and desktop.”)

範例：
**Context:** You are an expert full-stack developer using Lovable.  
**Task:** Create a secure login page in React using Supabase (email/password auth).  
**Guidelines:** The UI should be minimalistic, and follow Tailwind CSS conventions. Provide clear code comments for each step.  
**Constraints:** Only modify the `LoginPage` component; do not change other pages. Ensure the final output is a working page in the Lovable editor.



### 問題回顧
Summarize the errors we encountered setting up JWT authentication and explain how we resolved them. Then, draft a prompt I could use in the future to avoid those mistakes when setting up auth.


## prompt
我邊看文章，邊想一個讓AI幫我想prompt的prompt：


> [!NOTE] Title
> 幫我想一段用來把基礎描述轉換成高效 AI prompt 的 prompt ，他要能夠列出這些需求： 
> 1. 清楚而且直接，不能有模糊或條件判斷的空間 
> 2. 有邏輯，列出每一個單位可執行步驟並且解釋，之後一步一步執行。 
> 3. 回顧檢查有沒有不清楚的地方 
> 4. 不能有假設空間，發現自己在猜測使用者目標的情況時，需要要求使用者給出更詳細的指示

以下是chatgpt回給我的：

下面這段可以直接貼給任何能讀繁體中文的 LLM。它會把你貼上的「基礎描述」（放在三個反引號內）轉成一個**高效、可直接執行**的 AI prompt，並依序**拆解、解釋、執行、檢查**。它完全遵守你列出的 4 項要求（不模糊、有邏輯、回顧檢查、不得自行假設）。直接複製整段並在最後把基礎描述放入三個反引號中即可。

你現在的角色：Prompt 工程師（Output-first）。任務：把使用者提供的「基礎描述」（以三個反引號包起來）轉換成一個高效、可直接貼入並執行的 AI prompt，並依下列流程**一步步執行**。全部回覆請使用繁體中文，且不得使用模糊、條件或推測語句（例如：可能、或許、如果、視情況而定、猜測等詞）。流程如下：

A. 直接重述（不推測）
1. 以一句**明確且不帶假設**的句子重述我收到的基礎描述（僅限描述內容，不加任何補充或推論）。

B. 欄位檢查（必要項目先行）
2. 列出「必要輸入欄位」與「可選輸入欄位」。對於每個必要欄位，寫出範例格式（例如：文字、JSON、長度限制、範例值）。
3. 若有任何**必要欄位缺失**，**立即停止後續執行**，以清單形式提出**精確可直接複製的問題**讓使用者補充（每一項都要能直接回答或貼上）。不得自行填補或假設缺少的資訊。

C. 拆解成可執行步驟（逐步且有說明）
4. 將整個任務拆成「最小可執行步驟單位」，每個步驟使用數字編號。每個步驟必須包含：
   - 步驟名稱（短語）
   - 目的（1 句清楚動作目標）
   - 輸入（該步驟需要哪些明確資料／欄位）
   - 輸出（完成後會得到的具體產物或格式）
   - 可直接執行的指令句（可貼給 LLM 或自動化系統）
   - 1–2 句解釋：為何要這麼做（簡短、具體）
5. 完成上述拆解後，**立刻開始按序執行第 1 步、第 2 步…**（只有在所有必要輸入都已確認存在時執行）。每一步執行完畢都須回傳該步驟的「輸出內容」。

D. 產出最終高效 Prompt（可直接使用）
6. 生成一個乾淨、可直接貼入 LLM 的最終 prompt，格式要包含：
   - 執行前檢查清單（列出必要欄位）
   - 明確任務說明（動詞導向，無模糊語句）
   - 約束條件（輸出格式、長度、風格等）
   - 範例輸入與範例輸出（短範本）
   - 如需多輪追問，列出每一輪要問的明確問題（但依規則：若必要欄位缺失，不要自動問假設性的問題，直接停止並請使用者回答）

E. 回顧與驗證（完成後）
7. 列出「所有你避免的假設」（那些你本來可能會猜測但沒有做的事），以及「仍存在的不清楚處／風險」。
8. 提供 3 個具體且可執行的驗證檢查點或測試方法，用以確認最終結果是否符合需求（例如：檢查欄位 X 是否為 ISO 日期、檢查長度、檢查語氣是否為正式）。

F. 回應風格限制
9. 回覆必須使用命令式、明確語句，**嚴禁**使用下列類型的詞彙或表達：可能、或許、如果、視情況、猜測、應該、可能會、看起來。因此所有指示需呈現為可執行的具體步驟或明確的問題。

輸出格式建議（機器可讀 JSON 範例）：
{
  "summary": "...",
  "required_inputs": [{"name":"...","format":"...","example":"..."}],
  "steps":[
    {"id":1,"name":"...","purpose":"...","input":"...","output":"...","command":"...","explain":"..."},
    ...
  ],
  "final_prompt":"(可直接貼入 LLM 的字串)",
  "execution_results":[{"step":1,"output":"..."}, ...],
  "review":{"avoided_assumptions":[...],"open_questions":[...],"validation_checks":[...]}
}

現在請把你要轉換的基礎描述放在三個反引號內並貼給我（我會依上述流程執行）。




附註（建議）

- 若想讓生成的 prompt 更精準，請在基礎描述中附上「期望輸出格式範例」或「最小可接受標準」。
    
- 你可以把任何基礎描述直接貼上來，我會立即依上述流程幫你轉換並執行第一輪拆解與檢查（如缺資訊會停止並列出需補充的精確問題）。
    

需要我現在幫你把某段基礎描述轉成高效 prompt 嗎？直接把描述貼上來就行。