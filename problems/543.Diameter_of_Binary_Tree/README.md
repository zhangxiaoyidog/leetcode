## 543.Diameter of Binary Tree

## 题目描述

给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

**示例 :**
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

**注意：**两结点之间的路径长度是以它们之间边的数目表示。



### 解答

​	这道题和[124](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/124.Binary_Tree_Maximum_Path_Sum/README.md)的做法是一样的，递归去寻找左边的最大路径和以及右边的最大路径，然后判断在该节点包含左右子树的路径是否大于当前最大路径和，最终找出最大的路径。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        def get_max(root):
            if root==None:
                return 0
            left = get_max(root.left)
            right = get_max(root.right)
            self.path = max(self.path,left+right+1)
            return max(left,right)+1
        self.path = 0
        get_max(root)
        # 不包括根节点
        return self.path-1 if self.path>0 else 0
```

