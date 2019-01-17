## 102.Binary Tree Level Order Traversal

## 题目描述

给定一个二叉树，返回其按层次遍历的节点值。 （即逐层地，从左到右访问所有节点）。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```



### 解答

关于树的题目，大致可以分为两种:

+ 使用递归来解决(先序遍历，中序遍历，后序遍历……)
+ 使用迭代的方式，借助特殊的数据结构比如栈和队列等(层次遍历……)



​	这道题是关于树的层次遍历的，但是在层次遍历的同时需要按层取存储并返回结果，所以在入队的时候需要同时记录层数，然后加入到对应的层里面去，这里哪一层的判断是有一定的技巧性的。

​	还有一种方法是不记录层数，每次循环这一层的节点，也就是在while下面加一个for循环，每个循环把一层的节点遍历，然后把这一层的节点下一层的节点，也就是它们的孩子们入队，在下一次去循环，这样也能达到解决问题的目的。这个解法在下一题目中有使用，具体看下一题。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
import queue
class Solution:
    def levelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res = []
        if root == None:
            return res
        # 层次遍历需要用队列来解决问题,同时需要记录层数
        q = queue.Queue()
        q.put((root,0))
        while not q.empty():
            temp_node,level = q.get()
            if level == len(res):
              res.append([])
              
            res[level].append(temp_node.val)
            # 左子树和右子树的root入队
            if temp_node.left!=None: 
                q.put((temp_node.left,level+1))
            if temp_node.right!=None: 
                q.put((temp_node.right,level+1))
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 





​	