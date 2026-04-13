---
tags: []
date: 2026-04-10
time: 21:45
link: https://react.dev/learn
---


[[2026-04-10|2026-04-10 Fri, 21:45]]

react 哲學中常會提到一種 SSOT(single source of truth) 或是 DRY (don't repeat yourself) 的概念，代表如果一個資料是藉由其他原始資料計算出來的話，就不要另外宣告，而是透過計算來取得。
- Thinking in React - Step 3: Find the minimal but complete representation of UI state [](https://react.dev/learn/thinking-in-react#step-3-find-the-minimal-but-complete-representation-of-ui-state "Link for Step 3: Find the minimal but complete representation of UI state")
- Managing State - Choosing the state structure [](https://react.dev/learn/managing-state#choosing-the-state-structure "Link for Choosing the state structure")
	- Full name 不要自己一個 state ，用 first name, last name 組合
- [Principles for structuring state](https://react.dev/learn/choosing-the-state-structure#principles-for-structuring-state)


[[2026-04-13|2026-04-13 Mon, 14:02]]

[great front end](https://www.greatfrontend.com/questions/user-interface/selectable-cells?practice=practice&tab=coding)
selected grids 的問題，我遇到了 ref, state 該用誰的問題。基本上 `{x, y}` 不會立刻改變 UI ，所以可以用 ref。