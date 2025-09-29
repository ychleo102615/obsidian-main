---
tags: []
date: 2025-09-29
time: 12:37
---

https://ithelp.ithome.com.tw/articles/10203788 
https://www.scaler.com/topics/list-comprehension-in-python/

```python
# in-place construction 
arr1 = [i for i in range(10)] 
# you can use if to filter the elements 
arr2 = [x for x in arr1 if x % 2 == 0] 
# you can use as many conditions as you want! 
arr3 = [x for x in arr1 if x >= 3 and x % 2] 
# use nested for loops to make everyone dizzy XD 
arr4 = [(x, y) for x in range(3) for y in range(4)]
```

