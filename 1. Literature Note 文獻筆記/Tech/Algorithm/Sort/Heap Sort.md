要先了解[[Binary Heap]]的資料結構。

# 步驟一：將矩陣轉換成Max Heap

## 使用函式：MaxHeapify、BuildMaxHeap轉換
走訪從root到最後一個含有子樹的node（index為size / 2），比較node, left child, rich child，使root成為最大值的那個。

# 步驟二  Heap Sort(堆積排序法)

如何將此Max Heap做排序呢？
Max Heap的特徵是「第一個node具有最大值」，如果要將資料「由小到大」排序，步驟如下：

1.  把「第一個node」和「最後一個node」互換位置。
2.  **假裝heap的「最後一個node」從此消失不見**。
3.  對「第一個node」進行`MaxHeapify()`。


# 時間複雜度
By the way, building a simple binary heap only takes 𝑂(𝑛) time. See: [Binary heap](http://en.wikipedia.org/wiki/Binary_heap#Building_a_heap "en.wikipedia.org")
Construction: 𝑂(𝑛), you have to do this only once.
Removing an element 𝑂(log(𝑘)) if you have k elements in heap.
Removing n elements
𝑂(log(𝑛)+log(𝑛−1)+log(𝑛−2)+....+log(1))=𝑂(log(𝑛!))=𝑂(𝑛log(𝑛))
Last reduction is called [Stirling's approximation](https://en.wikipedia.org/wiki/Stirling%27s_approximation "en.wikipedia.org").
So total time 𝑇(𝑛)=𝑂(𝑛)+𝑂(𝑛log(𝑛))=𝑂(𝑛log(𝑛))

[來源](https://www.quora.com/How-does-Heapsort-take-O-nlogn-time)
