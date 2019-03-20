## 111.Minimum Depth of Binary Tree

## 题目描述

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最小深度  2.

### 解答

​	这道题跟104题很相似，这道题是求最小深度，也是用递归去解，但是这里有一个特殊情况为假如左子树或右子树为空的情况，比如[1,2]，由于最小深度是从根节点到最近**叶子**节点的最短路径上的节点数量，所以这里最小深度为2。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root == None:
            return 0
        # 两种特殊情况
        if root.left == None:
            return self.minDepth(root.right)+1
        if root.right == None:
            return self.minDepth(root.left)+1 
        return min(self.minDepth(root.left)+1,self.minDepth(root.right)+1)
        
```

