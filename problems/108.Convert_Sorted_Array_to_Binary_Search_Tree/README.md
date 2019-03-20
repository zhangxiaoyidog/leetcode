## 108.Convert Sorted Array to Binary Search Tree

## 题目描述

将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```



### 解答

​	这道题是当然还是使用递归去解，每次要去找中间点作为root，然后中间点左边的作为左子树，右边的作为右子树，分别递归生成即可。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        # 递归解决，每次去找中间点作为root，左子树和右子树递归
        
        if len(nums)==0:
            return None
        
        # 找中间点
        mid_index = len(nums)//2
        root = TreeNode(nums[mid_index])
        
        root.left = self.sortedArrayToBST(nums[:mid_index])
        root.right = self.sortedArrayToBST(nums[mid_index+1:])
        return root
```

