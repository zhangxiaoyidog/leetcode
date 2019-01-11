## 098.**Validate Binary Search Tree**

## 题目描述

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

- 节点的左子树只包含**小于**当前节点的数。
- 节点的右子树只包含**大于**当前节点的数。
- 所有左子树和右子树自身必须也是二叉搜索树。

**示例 1:**

```
输入:
    2
   / \
  1   3
输出: true
```

**示例 2:**

```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
```



### 解答1

​	这道题当然也是使用递归算法求解了，递归判断左子树和右子树是否为二叉搜索树，但是也是需要判断第一条特性和第二条特性是否成立，如何让判断呢，这里使用了一个技巧，那就是先定义一个数为最小的浮点数，递归判断它是否比root和右子树中的值小，是就更新，否则会返回False。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
import sys
class Solution:
    last_val = -sys.float_info.max
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        
        # print(self.last_val)
        if root == None:
            return True
        
        if self.isValidBST(root.left):
            if self.last_val < root.val:
                self.last_val = root.val
                if self.isValidBST(root.right):
                    return True
        return False
```



### 解答2

​	对于这道题目，也可以选择递归分治法来解决，共有三个判断条件，第三个直接用递归就行，而1和2是遍历节点时的操作因子，那么我们可以用递归来遍历左子树和右子树，判断左子树的节点是否比当前节点小，右子树的节点是否比当前节点大，当然这里有一个小陷阱，我们有的同学可能会说，你直接递归判断1和2就是了，所以这里要注意的是假如只满足1和2并不一定就是二叉搜索树的，因为它的子树可能就不满足1和2了，这里可以自己举例去验证一下，就不多说，所以三个条件也是缺一不可，递归需要考虑的几个问题：递归停滞的条件，调用递归方法需要传递哪些参数，函数的返回值。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
import sys
class Solution:
    last_val = -sys.float_info.max
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if root == None:
            return True
        # 递归判断左子树和右子树
        left = self.isValidBST(root.left)
        right = self.isValidBST(root.right)
        
        # 遍历左子树的值
        if root.left!=None:
            if not self.left_isvalid(root.left,root.val):
                return False
        # 遍历右子树的值
        if root.right!=None:
            if not self.right_isvalid(root.right,root.val):
                return False
        return True
    
    
    def left_isvalid(self,node,val):
        if node == None:
            return True
        if node.val>=val:
            return False
        if self.left_isvalid(node.left,val) and self.left_isvalid(node.right,val):
            return True
    def right_isvalid(self,node,val):
        if node == None:
            return True
        if node.val<=val:
            return False
        if self.right_isvalid(node.left,val) and self.right_isvalid(node.right,val):
            return True    
```

