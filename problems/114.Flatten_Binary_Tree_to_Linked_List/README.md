## 114.Flatten Binary Tree to Linked List

## 题目描述

给定一个二叉树，[原地](https://baike.baidu.com/item/%E5%8E%9F%E5%9C%B0%E7%AE%97%E6%B3%95/8010757)将它展开为链表。

例如，给定二叉树

```
    1
   / \
  2   5
 / \   \
3   4   6
```

将其展开为：

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```



### 解答

​	这种树的题目首先要考虑使用递归的方式去解决，比较直观方便，递归展开左子树和右子树，然后把展开后的左子树接到root的right，右子树接到原来的左子树最后一个节点上，但是这里处理完记得要将left置空，否则会出错。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def flatten(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        # 使用递归来解决
        if root == None:
            return
        # 递归展开左子树和右子树
        self.flatten(root.left)
        self.flatten(root.right)
        # 把左子树接到root上，右子树接到左子树最后一个节点上
        temp_right = root.right
        root.right = root.left
        # 这里记得把left置空
        root.left = None
        flag = root
        while flag.right!=None:
            flag = flag.right
        flag.right = temp_right
        
```

