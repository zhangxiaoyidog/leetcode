## 199.Binary Tree Right Side View

## 题目描述

给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

**示例:**

```
输入: [1,2,3,null,5,null,4]
输出: [1, 3, 4]
解释:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```



### 解答

​	这道题其实就是找出最右侧的节点值，那么我们可以使用层次遍历，每层找到最右边的节点值，那么每层节点入栈时候先进右孩子节点就可以了。这道题也可以采用dfs去做，利用层数信息。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        # 也就是每层最后一个节点,采用层次遍历
        stack = []
        res = []
        if root!=None:
            stack.append(root)
            
        while len(stack)!=0:
            for r in range(len(stack)):
                this_node = stack[0]
                stack.pop(0)
                if r==0:
                    res.append(this_node.val)
                if this_node.right!=None:
                    stack.append(this_node.right)
                if this_node.left!=None:
                    stack.append(this_node.left)
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 