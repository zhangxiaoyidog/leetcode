## 144.Binary Tree Preorder Traversal

## 题目描述

给定一个二叉树，返回它的 *前序* 遍历。

 **示例:**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
```

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？



### 解答1

​	第一种解法就是使用递归算法啦，和之前做过的中序遍历一样，代码模板都一样，简单直观。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # 递归实现
        if root == None:
            return []
        
        res = []
        return self.preTrave(root, res)
    
    def preTrave(self, root, res):
        if root==None:
            return
        
        res.append(root.val)
        self.preTrave(root.left,res)
        self.preTrave(root.right,res)
        return res
```



### 解答2

​	第二种解法就是迭代算法，使用栈来帮助解题，一般这种不是用递归肯定是要使用栈或者队列等数据结构来做的，具体看代码，也比较简单。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def preorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        # 迭代算法,使用一个栈，进栈顺序为根节点，右孩子，左孩子
        if root == None:
            return []
        res = []
        
        stack = []
        stack.append(root)
        while stack:
            # 访问当前根节点
            this_node = stack.pop(-1)
            res.append(this_node.val)
            if this_node.right:
                stack.append(this_node.right)
            if this_node.left:
                stack.append(this_node.left) 
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$