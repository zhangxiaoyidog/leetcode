## 429.N-ary Tree Level Order Traversal

## 题目描述

给定一个 N 叉树，返回其节点值的层序遍历。 (即从左到右，逐层遍历)。

例如，给定一个 3叉树 :

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/narytreeexample.png)

返回其层序遍历:

[
     [1],
     [3,2,4],
     [5,6]
]


说明:

1. 树的深度不会超过 1000。
2. 树的节点总数不会超过 5000。



### 解答



```python
"""
# Definition for a Node.
class Node(object):
    def __init__(self, val, children):
        self.val = val
        self.children = children
"""
class Solution(object):
    def levelOrder(self, root):
        """
        :type root: Node
        :rtype: List[List[int]]
        """
        # print(root.children)
        res = []
        stack = []
        if root==None:
            return stack
        stack.append(root)
        while stack:
            res.append([])
            for i in range(len(stack)):
                cur_node = stack.pop(0)
                res[-1].append(cur_node.val)
                for j in range(len(cur_node.children)):
                    stack.append(cur_node.children[j])
        return res
            
```

