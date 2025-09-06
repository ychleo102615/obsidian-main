---
tags: 
date: 2023-11-15-週三
time: 14:34
---
從下面幾個連結可以知道，Lua 沒有循環引用的問題
# [Garbage Collection Tutorial](http://lua-users.org/wiki/GarbageCollectionTutorial)
Lua使用`Mark and sweep`的方式做GC。Unreachable的資料不會被標記到，因而能夠被回收。
# [Weak Tables](https://www.lua.org/pil/17.html)
# [Weak Tables Tutorial](http://lua-users.org/wiki/WeakTablesTutorial)


使用情境
[Weak Tables in lua - What are the practical uses?](https://stackoverflow.com/questions/10885741/weak-tables-in-lua-what-are-the-practical-uses)
```
Weak tables are often used in situations where you wish to give a name to a value without locking the value into existence, which takes up memory.
```

總結來說，weaktables是一種保險機制。在開發者能完全掌握物件週期的情況可能會覺得沒什麼用。

> [!NOTE] GPT
> 所以weak table充其量算是一個保險而已？
> ChatGPT
> 
> 沒錯，`weak table` 可以說是一種保險措施。它提供了一種機制，可以在管理物件引用時，更容易地確保不再被其他部分所引用的物件能夠被垃圾回收。這樣做可以幫助避免一些潛在的問題，例如內存洩漏，特別是在跟事件監聽器、快取系統或資源管理等相關的情境中。
> 
> 使用弱引用表能夠更靈活地管理記憶體，但同時也需要謹慎使用。它並不是解決所有問題的魔法解決方案，但在特定情況下，能夠幫助你更有效地管理記憶體資源，防止潛在的內存洩漏問題。
> 


### 額外補充
Lua的String本質上雖然是Object，但是使用起來是Value，就跟number, boolean一樣。
