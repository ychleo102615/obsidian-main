- [ ] [參考](https://alrightchiu.github.io/SecondRound/comparison-sort-heap-sortdui-ji-pai-xu-fa.html)

## 特徵一：完全二元樹
---
若二元樹的高度(深度)為 h，除第 h 層外，其他各層(1 ~ h-1)的節點數都達到最大個樹，而第 h 層從右向左連續缺幾個節點，則這個二元樹就稱 **完全二元樹**。

這樣的優點是方便尋找「parent-child」之關係，以index(i)的node為例：

-   其**left child**必定位在**index(2i)**；
-   其**right child**必定位在**index(2i+1)**；
-   其**parent**必定位在**index(⌊i/2⌋)**。

![[Pasted image 20230417223622.png]]

## 特徵二：親子規則
-   **Max Heap**：在每一個subtree中，**root**之「數值」要比兩個**child**之「數值」還要大：
    
    -   value(i)>value(2i)
    -   value(i)>value(2i+1)
-   **Min Heap**：在每一個subtree中，**root**之「數值」要比兩個**child**之「數值」還要小：
    
    -   value(i)<value(2i)
    -   value(i)<value(2i+1)


# MaxHeapify
[[2024-08-10|2024-08-10, 12:57]]

[insert and extract max](https://www.shubo.io/binary-heap/)
[sink swim algorithm](https://mathcenter.oxford.emory.edu/site/cs171/sinkAndSwim/)

# [為什麼heapify只需要O(n)](https://stackoverflow.com/questions/9755721/how-can-building-a-heap-be-on-time-complexity)

這是一個數學算出來的時間
