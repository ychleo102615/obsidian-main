## 原理
使用Pivot來Divide & Conquer的演算法，小的放pivot左邊，大的放pivot右邊。
Quick Sort 的核心思想就是：**挑基準點，把數據分成左右兩堆，然後對每堆再做同樣的事情，最後合起來。**
https://chatgpt.com/share/6754627e-c72c-8008-96bc-dd5b7be6339a

## 表現
### 平均：O(nlogn)
### 最差 O(n^2)
[參考](https://www.baeldung.com/cs/quicksort-time-complexity-worst-case)
quick sort會把資料分成兩塊，如果資料被分的極度不平均，那會容易變成worst case

## 適用性
不適合用在資料全都一樣、或是已經排好序的資料。

## 優化
1. 挑好一點的pivot，挑到剛好是最大的話可能會導致worst case。
2. partitioning的方式，常見的有兩種：**Hoare partition scheme** and **Lomuto Partition Scheme**
	- 前者較能降低swap的次數 [參考](https://www.techiedelight.com/quick-sort-using-hoares-partitioning-scheme/)
	- 需注意遞迴的範圍和 Lomuto Partition Scheme 的實作不同，因前者無法排出pivot元素，下次的遞迴中也必須要重算此次pivot的位置
	- 有些不同的[實踐法](https://ithelp.ithome.com.tw/articles/10278644)
 
[參考](https://www.techiedelight.com/boost-quicksort-performance/)


2023-06-23-週五, 17:30
---

[leetcode](https://leetcode.com/problems/sort-an-array/submissions/977732496/)
```cpp
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        quicksort(nums, 0, nums.size() - 1);
        return nums;
    }

    void quicksort(vector<int>& nums, int start, int end) {
        if (start >= end) {
            return;
        }
        int pivot = partition(nums, start, end);

        quicksort(nums, start, pivot);
        quicksort(nums, pivot + 1, end);
    }

    int partition(vector<int>& nums, int& start, int& end) {
        /*
        這邊我很納悶為什麼要退進一格，還有為什麼不直接用while。
        跑完發現，如果不用do while的方式，left指的值還是比pivot小，這樣交換是錯的。
        */
        int left = start - 1;
        int right = end + 1;

        int pivot = getMiddle(nums, start, end);
        // int pivot = nums[start];

        while(1) {
            // while(nums[left] < pivot) {
            //     left++;
            // }
            // while(nums[right] > pivot) {
            //     right--;
            // }
            do { left++; } while (nums[left] < pivot);
            do { right--; } while (nums[right] > pivot);
            if (left >= right) {
                /*
                最終，left, right之間的值，應該都是pivot
                回傳誰回去當quick sort的pivot，要看quicksort的範圍
                以目前的程式碼來說，回傳left回去會導致partition前後都有現在的pivot值，分的不乾淨
                */
                return right;
            }
            myswap(nums[left], nums[right]);
        }
        return start;
    }

    int getMiddle(vector<int>& nums, int& start, int& end) {
        int middle = (start + end) / 2;
        int max = (nums[start] > nums[middle]) ? nums[start] : nums[middle];
        return (max < nums[end]) ? max : nums[end]; 
    }

    void myswap(int& a, int& b) {
        int temp = a;
        a = b;
        b = temp;
    }
};
```