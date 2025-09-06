---
tags:
  - 1D-dp
  - 2D-dp
date: 2025-04-13
time: 15:07
---

| 解法                   | 何時表現較好               | 特點             |
| -------------------- | -------------------- | -------------- |
| DFS + memoization    | 狀態空間稀疏、有明顯剪枝空間       | 探索必要狀態，記憶化防重複  |
| Bottom-up 2D DP      | 狀態空間密集，大部分子問題都會用到    | 強制填表，記憶體消耗大但穩定 |
| Bottom-up 1D DP (壓縮) | 可壓縮空間時（如不需要舊狀態以外的資訊） | 時間相同但空間更省      |

| Approach          | Best Used When…                                             |
| ----------------- | ----------------------------------------------------------- |
| DFS + Memoization | Large state space, lots of invalid states, pruning possible |
| 2D Bottom-up DP   | Most states are useful, transitions are regular             |
| 1D Bottom-up DP   | Like 2D DP, but with memory optimization when possible      |

## ✅ 常見題型 vs 解法選擇對照表（DFS vs DP）

| 題型類別                       | 建議解法                      | 原因與判斷依據                     | 範例題目（Leetcode）                                                            |
| -------------------------- | ------------------------- | --------------------------- | ------------------------------------------------------------------------- |
| 最長子序列（Longest Subsequence） | 2D DP → 1D DP（壓縮）         | 狀態密集，所有狀態幾乎都會用到             | [[1143. Longest Common Subsequence]]                                      |
| 有大量無效解可剪枝的組合問題             | DFS + Memoization + Prune | 有條件可提早終止、部分解無需展開            | [[131. Palindrome Partitioning]]<br>698. Partition to K Equal Sum Subsets |
| 需要回傳所有解（而非計算最佳解）           | DFS (Backtracking)        | DFS 更適合列舉所有可能的解             | [[39. Combination Sum]]                                                   |
| 有明確轉移方程且狀態空間不大             | Bottom-up DP              | 無需剪枝，且每個子問題都重要              | [[518. Coin Change II]]                                                   |
| 子字串或子陣列類問題（連續性需求）          | 1D 或 2D Bottom-up DP      | 可利用連續性的轉移，memo 空間優化效果不顯著    | [[53. Maximum Subarray]]                                                  |
| 二維區間DP（如切割類問題）             | DFS + Memo 或 2D DP        | 根據區間長度建表，或透過 DFS 尋找區間最佳分割策略 | [[312. Burst Balloons]]                                                   |
