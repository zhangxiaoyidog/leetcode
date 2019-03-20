## 112.Path Sum

## 题目描述

给定一个二叉树和一个目标和，判断该树中是否存在根节点到叶子节点的路径，这条路径上所有节点值相加等于目标和。

**说明:** 叶子节点是指没有子节点的节点。

**示例:** 
给定如下二叉树，以及目标和 `sum = 22`，

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1

```

返回 `true`, 因为存在目标和为 22 的根节点到叶子节点的路径 `5->4->11->2`。

### 解答

​	这道题的话比较简单的方法就是直接递归去做，判断此节点是否为叶子节点的同时，并且路径上的数字和等于所给的sum，然后递归判断它的左子树和右子树的节点，也就是DFS求解的过程，也有比较麻烦的方式比如先序遍历的同时去记录和判断，可以自己尝试一下。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def hasPathSum(self, root, sum):
        """
        :type root: TreeNode
        :type sum: int
        :rtype: bool
        """
        if root == None:
            return False
        # 这里必须是叶子结点
        if root.left == None and root.right == None and root.val == sum:
            return True
        #　递归求解
        return self.hasPathSum(root.left,sum-root.val) or self.hasPathSum(root.right,sum-root.val)
        
```

