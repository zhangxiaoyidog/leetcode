## 226.Invert Binary Tree

## 题目描述

翻转一棵二叉树。

**示例：**

输入：

```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```

输出：

```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```



### 解答

​	这道题比较简单，使用递归的方法去解决就好了。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        # 递归
        if root == None:
            return root
        temp_node = root.left
        # 1
        # root.left = root.right
        # root.right = temp_node
        # if root.left!=None:
        #     self.invertTree(root.left)
        # if root.right!=None:
        #     self.invertTree(root.right)
        # 2
        root.left = self.invertTree(root.right)
        root.right = self.invertTree(temp_node)
        return root
```

