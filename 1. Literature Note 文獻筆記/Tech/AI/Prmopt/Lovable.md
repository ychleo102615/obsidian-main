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