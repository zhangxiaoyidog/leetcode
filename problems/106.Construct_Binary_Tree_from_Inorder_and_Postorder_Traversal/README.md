## 106.Construct Binary Tree from Inorder and Postorder Traversal

## 题目描述

根据一棵树的中序遍历与后序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

例如，给出

```
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```



### 解答

​	这道题还是跟上道题的套路一样，使用递归求解，每次找好根节点，也就是分界点，然后把左子树的列表和右子树的列表放进去递归就ok了。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, inorder, postorder):
        """
        :type inorder: List[int]
        :type postorder: List[int]
        :rtype: TreeNode
        """
        
        # 递归解决
        if len(inorder) == 0 or len(postorder) == 0:
            return None
        
        root = TreeNode(postorder[-1])
        # 找到分界点
        divided_node = inorder.index(root.val)
        # 递归构造左子树和右子树
        root.left = self.buildTree(inorder[:divided_node],postorder[:divided_node])
        root.right = self.buildTree(inorder[divided_node+1:],postorder[divided_node:-1])
        
        return root
```

