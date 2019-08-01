## 437.Path Sum III

## 题目描述

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

**示例：**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

  	  10
 	 /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1. 5 -> 3
2. 5 -> 2 -> 1
3. -3 -> 11
```



### 解答

​	这道题双重递归，首先以根节点为起始点向下搜索，然后再以它的孩子节点为起点向下搜索寻找满足条件的路径。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def __init__(self):
        self.res = 0
    def pathSum(self, root: TreeNode, sum: int) -> int:
        if root==None:
            return 0
        self.child_search(root, sum)
        self.pathSum(root.left, sum)
        self.pathSum(root.right, sum)
        
        return self.res
    def child_search(self,root, sum):
        if root==None:
            return
        if sum==root.val:
            self.res+=1
        self.child_search(root.left, sum-root.val)
        self.child_search(root.right, sum-root.val)
```

