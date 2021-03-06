## 450.Delete Node in a BST

## 题目描述

给定一个二叉搜索树的根节点 root 和一个值 key，删除二叉搜索树中的 key 对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

首先找到需要删除的节点；
如果找到了，删除它。
说明： 要求算法时间复杂度为 O(h)，h 为树的高度。

**示例:**

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7


给定需要删除的节点值是 3，所以我们首先找到 3 这个节点，然后删除它。

一个正确的答案是 [5,4,6,2,null,null,7], 如下图所示。

	5
   / \
  4   6
 /     \
2       7

另一个正确答案是 [5,2,6,null,4,null,7]。

	5
   / \
  2   6
   \   \
    4   7
```



### 解答

​	这道题还是需要用递归的方法去做，首先找到要删除的节点，判断它的左子树和右子树是否为空，假如其中一个为空，那么直接把另一边返回即可，即往上接，假如左右都不为空，那么我们需要把右子树最小的那个提出来作为新的root，然后把原来的左右子树接到新的root上。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:
        if root == None:
            return
        
        if key<root.val:
            root.left = self.deleteNode(root.left, key)
            return root
        elif key>root.val:
            root.right = self.deleteNode(root.right, key)
            return root
        else:
            if root.left==None:
                return root.right
            elif root.right==None:
                return root.left
            else:
                #左右子树都在，需要把右子树最小的那个提出来作为新的root
                temp1 = root.right
                # 找到这个节点
                while temp1.left:
                    temp1 = temp1.left
                # 删除这个节点
                temp1.right = self.deleteMin(root.right)
                temp1.left = root.left
                return temp1
            
    def deleteMin(self,node):
        if node.left==None:
            return node.right
        node.left = self.deleteMin(node.left)
        return node
```

