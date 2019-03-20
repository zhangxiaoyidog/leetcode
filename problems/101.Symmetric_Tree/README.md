## 101.Symmetric Tree

## 题目描述

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

```
    1
   / \
  2   2
   \   \
   3    3
```



### 解答

​	这道题要求判断是否是镜像对称的，那么我们可以递归判断兄弟节点的左子树和右子树是否对称来解决，具体看代码。但是这里的代码有一个问题是如果把根节点当成左右节点传入会导致每个节点判断两次，也就是遍历了两遍，所以修改代码把根节点的两个孩子节点传入即可解决，时间复杂度变低。

​	在评论区有看到使用非递归的方法解决的，大概思想是使用两个栈，首先不停遍历节点的左孩子和右孩子并且分别进两个栈，不同即返回False，然后再同时出栈遍历这两个节点的右孩子和左孩子，直到最后栈为空。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.isMirror(root,root)
    
    def isMirror(self,root1,root2):
        
        if root1==None and root2==None:
            return True
        
        if root1!=None and root2!=None and root1.val == root2.val:
            return self.isMirror(root1.left,root2.right) and self.isMirror(root1.right,root2.left)
        else:
            return False
```



---



```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root == None or (root.left==None and root.right==None):
            return True
        
        return self.isMirror(root.left,root.right)
    
    def isMirror(self,root1,root2):
        # 递归判断左子树和右子树
        if root1==None and root2==None:
            return True
        
        if root1!=None and root2!=None and root1.val == root2.val:
            return self.isMirror(root1.left,root2.right) and self.isMirror(root1.right,root2.left)
        else:
            return False 
```

