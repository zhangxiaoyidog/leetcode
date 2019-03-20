## 113.Path Sum II

## 题目描述

给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

```

返回:

```
[
   [5,4,11,2],
   [5,8,4,5]
]
```

### 解答

​	这道题跟112题很相似，但是这道题的难点在于需要记录符合条件的路径，我的思路还是不变，使用DFS递归的方式，在做这道题的时候我就想到能不能用我们之前提到的递归代码框架解决，其实是可以的，只是需要修改具体的细节即可，要注意的地方就是在加入res列表的时候必须是一个新的list，即使用list(……)的方法或者是下面的方法，这里一定要注意。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: List[List[int]]
        """
        if root == None:
            return []
        res = []
        res = self.dfs_path(root,sum,res,[])
        return res
    def dfs_path(self,root,sum,res,temp):
        if root == None:
            return
        if root.left == None and root.right == None and root.val == sum:
            # 这里传入必须是一个新list,下面也是
            res.append(temp+[root.val])
        if root.left != None:
            self.dfs_path(root.left,sum-root.val,res,temp+[root.val])
        if root.right != None:
            self.dfs_path(root.right,sum-root.val,res,temp+[root.val])
        return res
```

