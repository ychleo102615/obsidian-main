---
tags:
  - 1D-dp
  - 2D-dp
date: 2025-04-03
time: 15:26
---
### ✅ 使用 DP 的兩大條件：

1. **Overlapping Subproblems（重疊子問題）**  
    子問題會被重複計算 —— 這就是為什麼我們用記憶化（memoization）或表格（tabulation）來避免重複計算。
    
2. **Optimal Substructure（最適子結構）**  
    大問題的最佳解可以由子問題的最佳解組合出來。
    
這兩個條件都要滿足，才適合用 DP。


| 條件                                                 | 結論                                    |
| -------------------------------------------------- | ------------------------------------- |
| ✅ Optimal Substructure + ✅ Overlapping Subproblems | 適合用 DP                                |
| ✅ Optimal Substructure + ❌ No Overlapping          | 用 Divide and Conquer 更簡單有效            |
| ❌ No Optimal Substructure                          | 通常不適合用 DP（可能要用 greedy、backtracking 等） |