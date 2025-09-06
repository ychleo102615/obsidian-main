---
tags: 
date: 2024-05-06
time: 09:25
---
[[2024-05-06|2024-05-06, 09:26]]
## 5/2

LHDZ 還可能出錯的原因：
1. 確實有先進房間才收到updateRoomBet（因為後來發現，就算強制先收到updateRoomBet，也因遊戲設計本身，不會出錯）
2. chipsConfig應該沒有出錯，有出錯的話，在BetViewModel中，應該要被filter掉（就不會出現frame nil問題了）
3. 在不知道的條件下，BetChipsManager release了，或是重設setChipsConfig為nil?
4. 非正常斷線的情況下離開GameLayer
5. 瞬間連續進入遊戲兩次？