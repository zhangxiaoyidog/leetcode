## 222.Count Complete Tree Nodes

## 题目描述

给出一个**完全二叉树**，求出该树的节点个数。

**说明：**

[完全二叉树](https://baike.baidu.com/item/%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91/7773232?fr=aladdin)的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

**示例:**

```
输入: 
    1
   / \
  2   3
 / \  /
4  5 6

输出: 6
```



### 解答1

​	第一种解法就是采用层次遍历的方法，统计有多少节点就完事了。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countNodes(self, root: TreeNode) -> int:
        # 层次遍历
        node_nums = 0
        stack = []
        if root!=None:
            stack.append(root)
        
        while len(stack)!=0:
            this_node = stack.pop(0)
            node_nums+=1
            if this_node.left:
                stack.append(this_node.left)
            if this_node.right:
                stack.append(this_node.right)
        return node_nums
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 



###解答2

​	第二种解法就是采取分治法，利用递归的方式去统计。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countNodes(self, root: TreeNode) -> int:
        # 递归（分治）
        if root==None:
            return 0
        return self.countNodes(root.left) + self.countNodes(root.right) + 1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 