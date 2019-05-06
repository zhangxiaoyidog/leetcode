## 230.Kth Smallest Element in a BST

## 题目描述

给定一个二叉搜索树，编写一个函数 `kthSmallest` 来查找其中第 **k** 个最小的元素。

**说明：**
你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。

**示例 1:**

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 1
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 3
```


### 解答

​	这道题给定了一个二叉搜索树，要求找到第k小的元素，那么转化一下也就是中序遍历的第k个，所以使用递归(也可以使用非递归的方法)遍历第k个即可得到结果。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        # 中序遍历的第k个
        self.res = None
        self.count = 0
        self.inorder(root,k)
        return self.res
    
    def inorder(self,root,k):
        if root==None:
            return
        self.inorder(root.left,k)
        self.count+=1
        if self.count==k:
            self.res = root.val
            return
        self.inorder(root.right,k)

```

​	