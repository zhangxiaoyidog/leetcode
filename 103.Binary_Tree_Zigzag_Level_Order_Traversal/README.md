## 103.Binary Tree Zigzag Level Order Traversal

## 题目描述

给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回锯齿形层次遍历如下：

```
[
  [3],
  [20,9],
  [15,7]
]
```

### 解答

​	这道题跟上一道题的不同之处在于，这一道题在有些层需要从右往左遍历输出，也就是层与层之间交替进行，即先从左往右，再从右往左进行下一层遍历，以此类推。所以在上一题中提到的第二种思路在这里就很适合了，假如这一层需要倒序，加入到最终的res列表中时直接使用列表的倒序操作[::-1]就很方便了。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
import queue
class Solution:
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        res = []
        if root == None:
            return res
        # 层次遍历需要用队列来解决问题,偶数层倒序
        q = queue.Queue()
        q.put(root,0)
        odd = -1
        while not q.empty():
            level_list = []
            for _ in range(q.qsize()):
                temp_node = q.get()
                level_list.append(temp_node.val)
                if temp_node.left!=None: 
                    q.put(temp_node.left)
                if temp_node.right!=None: 
                    q.put(temp_node.right)
            if len(level_list)!=0:
                if odd == 1:
                    res.append(level_list[::-1])
                else:
                    res.append(level_list)
            odd = -odd
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 