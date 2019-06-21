## 337.House Robber III

## 题目描述

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

**示例 1:**

```
输入: [3,2,3,null,3,null,1]
     3
   /   \
   2   3
    \   \ 
     3   1
输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
```

**示例 2:**

```
输入: [3,4,5,1,3,null,1]
     3
    / \
   4   5
  / \   \ 
 1   3   1
输出: 9

解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
```

### 解答

​	这道题其实跟前两道题很像，只不过这个题的数据结构改成了二叉树，那么也是用递归，明确一个思想，假如在当前节点偷，那么它的左孩子和右孩子必然不能偷，假如在当前节点不偷，左孩子和右孩子可偷可不偷，在每个节点使用一个list[a,b]，第一个元素为不包括根节点的最大值，第二个为包括根节点的最大值，那么不包含根节点，最大值为两个子树的最大值之和，包含根节点，最大值为两个子树不包含根节点的最大值加上根节点的值。

​	评论区有一句话感觉很有道理，对解答递归的题目很有帮助，这里也记录下。**递归思想（不要深入递归函数体，只需知道递归函数的功能，以及找到跳出递归的边界条件）**

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rob(self, root: TreeNode) -> int:
        # 使用递归
        if root==None:
            return 0
        res = self.helper(root)
        return max(res)
    def helper(self,root):
        # 0表示不偷，1表示偷
        res = [0,0]
        if root == None:
            return res
        left = self.helper(root.left)
        right = self.helper(root.right)
        res[0] = max(left[0],left[1])+max(right[0],right[1])
        res[1] = left[0]+right[0]+root.val
        return res
```

