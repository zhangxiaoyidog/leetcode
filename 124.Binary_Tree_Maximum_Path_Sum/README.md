## 124.Binary Tree Maximum Path Sum

## 题目描述

给定一个**非空**二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径**至少包含一个**节点，且不一定经过根节点。

**示例 1:**

```
输入: [1,2,3]

       1
      / \
     2   3

输出: 6
```

**示例 2:**

```
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```



### 解答

​	有关于树的题目，一般都会有递归的解决方案，这个题看似很复杂，其实如果单从一个节点来考虑，无非就两种情况，对于任意一个节点, 如果最大和路径包含该节点，第一种是其左右子树中所构成的和路径值较大的那个加上该节点的值后向父节点回溯构成最大路径，第二种是左右子树都在最大路径中, 加上该节点的值构成了最终的最大路径。

​	那么我们就可以递归去寻找左边的最大路径和以及右边的最大路径和，然后判断在该节点包含左右子树的路径和是否大于当前最大路径和，最终找出最大的路径和。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxPathSum(self, root: 'TreeNode') -> 'int':
        self.res = float("-inf")
        self.getMax(root)
        
        return self.res
    
    def getMax(self,root):
        if root == None:
            return 0
        # 如果子树路径和为负则应当置0表示最大路径不包含子树
        left = max(self.getMax(root.left),0)
        right = max(self.getMax(root.right),0)
        # 判断在该节点包含左右子树的路径和是否大于当前最大路径和
        self.res = max(self.res, root.val+left+right)
        return max(left,right) + root.val
```



