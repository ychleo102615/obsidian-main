---
tags: 
date: 2024-01-25
time: 22:38
---
[link](https://www.shubo.io/iterative-binary-tree-traversal/)
# 三種 Iterative Binary Tree Traversal 的方法 (Inorder, Preorder, Postorder)

## preorder
前序 (preorder): 中 -> 左 -> 右
## inorder
中序 (inorder): 左 -> 中 -> 右
## postorder
後序 (postorder): 左 -> 右 -> 中


[[2024-02-11|2024-02-11, 21:50]]
在看[[105. Construct Binary Tree from Preorder and Inorder Traversal]] 題的時候，發現自己對這三種走法也沒有完全熟悉。
走法的敘述其實蠻容易搞混的。我後來發現，他是在描述**節點本身是何時被走過**（中）。

所以像BST排序，要使用inorder走才是對的，中間的值就應該在中間的順序。