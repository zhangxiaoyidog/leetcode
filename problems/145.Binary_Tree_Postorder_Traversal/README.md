## 145.Binary Tree Postorder Traversal

## 题目描述

给定一个二叉树，返回它的 *后序* 遍历。

**示例:**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [3,2,1]
```

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？



### 解答1

​	和上道题一样，还是同样的模板递归。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # 递归实现
        if root == None:
            return []
        
        res = []
        return self.postTrave(root, res)
    
    def postTrave(self, root, res):
        if root==None:
            return
        self.postTrave(root.left,res)
        self.postTrave(root.right,res)
        res.append(root.val)
        return res
```



###解答2

​	使用迭代算法和之前的类似，但是这里也有一些小小的不同，进栈顺序一样，但是访问顺序不一样，访问条件也不一样，假如当前节点为叶子节点或者上一个访问的节点是此节点的孩子节点，则访问并弹出。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def postorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # 迭代算法,使用一个栈，进栈顺序为根节点，右孩子，左孩子
        if root == None:
            return []
        res = []
        pre = None
        stack = []
        stack.append(root)
        while stack:
            # 访问但是不弹出当前根节点
            this_node = stack[-1]
            if this_node.left==None and this_node.right==None or (pre!=None and (pre==this_node.left or pre==this_node.right)):
                # 假如当前节点为叶子节点或者上一个访问的节点是此节点的孩子节点，则访问
                res.append(this_node.val)
                pre = this_node
                stack.pop(-1)
            else:
                if this_node.right:
                    stack.append(this_node.right)
                if this_node.left:
                    stack.append(this_node.left) 
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$