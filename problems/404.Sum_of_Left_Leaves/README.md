## 404.Sum of Left Leaves

### 题目描述

计算给定二叉树的所有左叶子之和。

**示例：**

      3
     /  \
    9    20
        /  \
       15   7
     
在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24



### 解答

​	这道题比较简单。重写一个方法递归就可以了，加一个标志位判断是否为左边。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
        if root==None or (root.left==None and root.right==None):
            return 0
        
        return self.judge(root.left,1) + self.judge(root.right,0)
    def judge(self,node,isleft):
        if node!=None and isleft:
            if node.left==None and node.right==None:
                return node.val
            return self.judge(node.left,1) + self.judge(node.right,0)
        elif node!=None:
            return self.judge(node.left,1) + self.judge(node.right,0)
        else:
            return 0
            
```

