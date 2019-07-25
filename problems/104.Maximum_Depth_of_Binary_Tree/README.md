## 104.Maximum Depth of Binary Tree

## 题目描述

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。



### 解答１

​	第一种解法就是递归，一颗二叉树的最大深度等于`max(左子树的最大深度，右子树的最大深度)+1`，代码比较简单。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        # 递归
        if root == None:
            return 0
        
        return max(1+self.maxDepth(root.left),1+self.maxDepth(root.right))
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(log(n))$



note：在最糟糕的情况下，树是完全不平衡的，*例如*每个结点只剩下左子结点，递归将会被调用 N 次（树的高度），因此保持调用栈的存储将是 O(N)。但在最好的情况下（树是完全平衡的），树的高度将是 log(N)。



### 解答2

​	第二种解法就是迭代的方式，使用一个栈保存访问到的节点和它的深度，即使用DFS的策略访问每个节点，同时在每次访问的时候更新最大深度。由此可见DFS只是一种策略，它有迭代和递归两种实现方式。注意这里用的是栈不是队列，所以是DFS。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        stack = []
        if root == None:
            return 0
        stack.append((1,root))
        depth = 1
        while len(stack)!=0:
            cur_depth,node = stack.pop()
            depth = max(depth,cur_depth)
            if node.left != None:
                stack.append((cur_depth+1,node.left))
            if node.right != None:
                stack.append((cur_depth+1,node.right))
        return depth
```

- 时间复杂度：$O(n)$.
- 空间复杂度：$O(n)$.