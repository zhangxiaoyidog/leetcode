## 129.Longest Consecutive Sequence

## 题目描述

给定一个二叉树，它的每个结点都存放一个 `0-9` 的数字，每条从根到叶子节点的路径都代表一个数字。

例如，从根到叶子节点路径 `1->2->3` 代表数字 `123`。

计算从根到叶子节点生成的所有数字之和。

**说明:** 叶子节点是指没有子节点的节点。

**示例 1:**

```
输入: [1,2,3]
    1
   / \
  2   3
输出: 25
解释:
从根到叶子节点路径 1->2 代表数字 12.
从根到叶子节点路径 1->3 代表数字 13.
因此，数字总和 = 12 + 13 = 25.
```

**示例 2:**

```
输入: [4,9,0,5,1]
    4
   / \
  9   0
 / \
5   1
输出: 1026
解释:
从根到叶子节点路径 4->9->5 代表数字 495.
从根到叶子节点路径 4->9->1 代表数字 491.
从根到叶子节点路径 4->0 代表数字 40.
因此，数字总和 = 495 + 491 + 40 = 1026.
```



### 解答1

​	这道题首先想到的是用递归的方式去解答，也就是再写一个方法递归，首先判断是否为空，是则返回0，然后判断此节点是否叶子节点，是则把之前所有的累加，这里也就是所有祖先节点的值加上当前值，否则继续累加乘以10，往下递归。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        if root==None:
            return 0
        return self.sumChilds(0,root)
    def sumChilds(self,cur_val,root):
        # 递归实现
        if root == None:
            return 0
        if root.left==None and root.right==None:
            return cur_val+root.val
        cur_val = (cur_val+root.val) * 10
        return self.sumChilds(cur_val,root.left) + self.sumChilds(cur_val,root.right)
```



```python
### 另一种写法
class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
        if root == None:
            return 0
        return self.sumChilds(0, root)

    def sumChilds(self, cur_val, root):
        if root == None:
            return 0
        if root.left == None and root.right == None:
            return cur_val * 10 + root.val
        return self.sumChilds(cur_val * 10 + root.val, root.left) + self.sumChilds(cur_val * 10 + root.val, root.right)
```





### 解答2

​	第二种解答则是非递归了，也可以用层次遍历的方式，但是无论递归还是非递归，都需要记录的是累加的值，以及判断是否是叶子节点，最后加起来。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sumNumbers(self, root: TreeNode) -> int:
		# 非递归实现
		if root == None:
            return 0
        q = []
        num_sum = 0
        q.append((root,root.val))
        while q:
            this_node,val = q.pop(0)
            if not this_node.left and not this_node.right:
                num_sum += val
            if this_node.left:
                q.append((this_node.left,this_node.left.val+val*10))
            if this_node.right:
                q.append((this_node.right,this_node.right.val+val*10))
        return num_sum
```

