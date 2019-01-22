## 107.Binary Tree Level Order Traversal II

## 题目描述

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其自底向上的层次遍历为：

```
[
  [15,7],
  [9,20],
  [3]
]
```



### 解答

​	这道题和102题很相似，但是这道题需要从最下面一层开始输出，所以最简单直接的方法就是把102的结果直接反转，但是这样做还不如直接在每层遍历结果插入时候就在index为0的位置插入就好了，所以在这个题中也学到了python列表有一个insert方法。

​	这道题正常的做法有很多，也可以先用一个字典把每一层的遍历结果给存起来，键存的是层号，值存的是对应层的数，最后再用一个for循环加入到最终的result中。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
import queue
class Solution:
    def levelOrderBottom(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
    
        if root == None:
            return []
        res = []
        
        q = queue.Queue()
        q.put(root)
        
        while not q.empty():
            level_list = []
            
            for _ in range(q.qsize()):
                temp_node = q.get()
                level_list.append(temp_node.val)
                if temp_node.left != None:
                    q.put(temp_node.left)
                if temp_node.right != None:
                    q.put(temp_node.right)  
            res.insert(0,level_list)
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 