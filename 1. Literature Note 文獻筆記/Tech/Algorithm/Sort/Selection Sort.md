
## 簡單來說，每次從未排序資料中找出最小的元素放到左邊，直到做完。

### 複雜度：O(n^2)

在寫leetcode時，遇到 [75. Sort Colors](https://leetcode.com/problems/sort-colors/description/) 這個問題，剛好順便了解一下。

```
template<class ForwardIt>
void selection_sort(ForwardIt begin, ForwardIt end)
{
    for (ForwardIt i = begin; i != end; ++i)
        std::iter_swap(i, std::min_element(i, end));
}
```
[來源](https://en.cppreference.com/w/cpp/algorithm/iter_swap)

2023/04/05 發現上面這樣我自己看不懂

[參考](https://medium.com/appworks-school/初學者學演算法-排序法入門-選擇排序與插入排序法-23d4bc7085ff)