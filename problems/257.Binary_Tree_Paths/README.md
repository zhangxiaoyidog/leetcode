## 257.Binary Tree Paths

## 题目描述

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

```
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```



### 解答

​	这道题还是使用熟悉的DFS搜索所有的路径就可以了。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        # 深度搜索
        res = []
        if root==None:
            return res
        temp = ''
        res = self.dfs_search(root,res,temp)
        return res
    def dfs_search(self,root,res,temp):
        if len(temp)==0:
            temp+=str(root.val)
        else:
            temp+='->'+str(root.val)
        
        if root.left==None and root.right==None:
            res.append(str(temp))
            return res
        if root.left:
            self.dfs_search(root.left,res,temp)
        if root.right:
            self.dfs_search(root.right,res,temp)
        return res
```

