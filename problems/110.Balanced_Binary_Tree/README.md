## 110. Balanced Binary Tree

## 题目描述

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点 *的左右两个子树的高度差的绝对值不超过1。

**示例 1:**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。
**示例 2:**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4

```

返回 `false` 。



### 解答

​	这道题比较简单，判断一个二叉树是否为平衡二叉树，只需要先判断根节点的左子树和右子树的高度高度差的绝对值是否超过一，然后递归判断左右子树是否为平衡二叉树即可，这里需要用到104题的二叉树的最大深度的递归求法。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root == None:
            return True
        
        # 递归判断左子树和右子树是否是平衡二叉树
        left_depth = self.maxDepth(root.left)
        right_depth = self.maxDepth(root.right)
        if left_depth-right_depth>1 or left_depth-right_depth<-1:
            return False
        else:
            return (self.isBalanced(root.left) and self.isBalanced(root.right))
    
    def maxDepth(self, root):
        """
        求树的最大深度
        """
        if root == None:
            return 0
        
        return max(self.maxDepth(root.left)+1, self.maxDepth(root.right)+1)
```

