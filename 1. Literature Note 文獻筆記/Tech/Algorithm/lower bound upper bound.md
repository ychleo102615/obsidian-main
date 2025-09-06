---
tags: 
date: 2024-12-13
time: 22:18
---
[lowerBound](https://en.cppreference.com/w/cpp/algorithm/lower_bound)：返回第一个**大於等於** `value` 的元素的位置，即“>= `value`”。
[upperBound](https://en.cppreference.com/w/cpp/algorithm/upper_bound)：返回第一个**大於** `value` 的元素的位置，即“> `value`”。

[[2025-08-09|2025-08-09 Sat, 14:37]]
回來寫題目，發現自己感覺又沒有完全搞懂。

現在我覺的用語意去來了解二元搜尋會很重要。因為這比較好理解，可能對與AI溝通也會有幫助。

我現在的想法是，要先搞清楚題目的本質，是給你「**下限**」還是「**上限**」。

給你下限的題目，就是不能比這個值小，但是越小越好。以視覺來理解的話，就是往左邊找。所以中間值使用`(l + r) // 2`就很直覺）。
```
----------
|  <--
----------
```

而給你上限的題目，就是不能比這個值大，但越大越好。視覺上往右邊找 ，中間值等於`(l + r + 1) // 2`。
```
----------
     --> |
----------
```

因為我們的關注點在於比較目標要 `>=` 或是 `<=`，所以目標值最好擺在我們要找的方向。

---
[[2025-03-03|2025-03-03 Mon, 23:57]]
關於下面敘述的洞見，後來有別的想法，來補充一下。
**excluding left, including right**是可以做的，只要改一下m的算法：
```python
[a, b]
l = 0
r = 1
m = (l+r+1)//2 # m == 1
```

另外整理一下二元搜尋的使用情境：

### 1. lower bound
要求：「尋找大於等於目標的值，越小越好」
### 2. time based store
就是下面的981題，要求：「尋找小於等於目標的值，越大越好」

### 3. rotated minimum
[[153. Find Minimum in Rotated Sorted Array]]
正常來說找最小值都是只要找左邊的值就好，這題是個特例，並且還能應用bs。
要求：「往**沒有**rotated的**另一半邊**收斂尋找最小值」，因為極值不會出現在沒有rotated的半邊裡（注意，這不代表極值就一定出現在有rotated的半邊裡，因為題目有可能沒有rotated）

[[2025-02-11]]
# 關於二元搜尋法Binary Search的洞見

我剛剛在解[[981. Time Based Key-Value Store]]這一題，他是分類在neetcode二元搜尋分類的題目。
這題就一般的情況是無法使用[[lower bound upper bound]]這種BS(binary search)的。

我想了一下為什麼。

這是因為這題的bs方向是**excluding left, including right**（搜尋條件：t 要小於等於timestamp，尋找最靠近timestamp的值），這是不符合lower bound演算法的。

lower bound的演算法是**including left, excluding right**的。這是由於我們計算middle值的方式是 `(l + r) // 2` ，middle是靠近left的。

設想長度只有2的陣列：
```python
[a, b]
l = 0
r = 1
m = (l+r)//2 # m == 0
```
如果對這樣的資料作**excluding left, including right**的BS的話，會陷入無窮迴圈或是`l > r`的窘況。
所謂**excluding left, including right**就是：
```python
r = m - 1 # excluding left
or
l = m # including right
```

而常見的**including left, excluding right**則是：
```python
r = m # including left
or
l = m + 1 # excluding right
```
這種BS方式不會進入死胡同，即是只有兩個元素也能好好的二分搜尋。

### 應用
當題目不符**including left, excluding right**時，將其反轉即可。

# 🎯簡單記憶建議
- 如果問題問的是 "**最小能達成條件**" → **正向 LB**
- 如果問題問的是 "**最大不超過條件**" → **反向 LB**