---
tags: []
date: 2026-01-18
time: 13:12
---

一個由大至小的數字陣列，我要怎麼有效率的由大至小檢查他們中取兩數的合？


這是一個經典問題！讓我直接說明最有效的方法。

## 核心思路：K 路合併 + Max Heap

假設陣列是 `[a₀, a₁, a₂, ..., aₙ₋₁]`（已由大到小排序）

**關鍵觀察**：把所有組合想成「多條已排序的序列」：

```
第 0 路（固定 a₀）：a₀+a₁, a₀+a₂, a₀+a₃, ...  ← 每路本身就是遞減的
第 1 路（固定 a₁）：a₁+a₂, a₁+a₃, a₁+a₄, ...
第 2 路（固定 a₂）：a₂+a₃, a₂+a₄, a₂+a₅, ...
...
```

這就變成了「合併 n-1 條已排序序列」的問題。

---

## 演算法步驟

````javascript
function* getPairSumsDescending(arr) {
  // arr 已經由大到小排序
  const n = arr.length;
  if (n < 2) return;
  
  // Max Heap：存放 [sum, i, j]，其中 i < j
  // 初始化：每一路的第一個元素
  const maxHeap = new MaxHeap();
  
  for (let i = 0; i < n - 1; i++) {
    maxHeap.push([arr[i] + arr[i + 1], i, i + 1]);
  }
  
  while (!maxHeap.isEmpty()) {
    const [sum, i, j] = maxHeap.pop();
    yield { sum, indices: [i, j] };  // 產出當前最大的和
    
    // 同一路的下一個候選者
    if (j + 1 < n) {
      maxHeap.push([arr[i] + arr[j + 1], i, j + 1]);
    }
  }
}
```
````
