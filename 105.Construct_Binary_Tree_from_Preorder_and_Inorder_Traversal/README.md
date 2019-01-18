## 105.Construct Binary Tree from Preorder and Inorder Traversal

## 题目描述

根据一棵树的前序遍历与中序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

例如，给出

```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
```

返回如下的二叉树：

```
    3
   / \
  9  20
    /  \
   15   7
```

### 解答

​	在之前没有做过这一类构造树的题目，虽然知道要用递归去做，但是还是有些无从下手，其实做了一些递归的题目之后，发现这一类题目的突破点在于分析怎么去把问题分解成同类的子问题。这一道题目重点在于找到切分点，也就是找到根节点后把两个list分为左子树和右子树部分去递归，最终达到解决问题的目的。

​	具体细节为preorder第一个元素为root，在inorder里面找到root，在它之前的为左子树（长l1），之后为右子树（长l2）。preorder[1]到preorder[l1]为左子树,之后为右子树，分别递归。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if len(preorder)==0 or len(inorder)==0:
            return None
        
        # 先序遍历的第一个元素肯定是root节点
        root = TreeNode(preorder[0])
        
        # 找到分割点
        root_index = inorder.index(root.val)
        # 递归构造左子树和右子树
        root.left = self.buildTree(preorder[1:root_index+1],inorder[0:root_index])
        root.right = self.buildTree(preorder[root_index+1:],inorder[root_index+1:])
        
        return root
```

