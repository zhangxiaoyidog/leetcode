## 094.**Binary Tree Inorder Traversal**

## 题目描述

给定一个二叉树，返回它的*中序* 遍历。

**示例:**

```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```



### 解答１

​	这种遍历二叉树的题目使用的首先当然是递归算法，非常简单直观，可以AC，之后也要尝试使用非递归算法来解答。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        if root == None:
            return []
        res = []
        res = self.inorder(res,root)
        return res
    def inorder(self,res,root):
        if root == None:
            return 
        else:
            self.inorder(res,root.left)
            res.append(root.val)
            self.inorder(res,root.right)
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

### 解答２

```python
#TODO 迭代(非递归)
```

