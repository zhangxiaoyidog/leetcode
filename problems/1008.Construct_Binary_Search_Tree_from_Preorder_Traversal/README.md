## 1008.Construct Binary Search Tree from Preorder Traversal

## 题目描述

返回与给定先序遍历 preorder 相匹配的二叉搜索树（binary search tree）的根结点。

(回想一下，二叉搜索树是二叉树的一种，其每个节点都满足以下规则，对于 node.left 的任何后代，值总 < node.val，而 node.right 的任何后代，值总 > node.val。此外，先序遍历首先显示节点的值，然后遍历 node.left，接着遍历 node.right。）

 

**示例：**

输入：[8,5,1,7,10,12]
输出：[8,5,10,1,7,null,12]

 ![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/03/08/1266.png)

**提示：**

1. 1 <= preorder.length <= 100
2. 先序 preorder 中的值是不同的。



### 解答

​	这道题不需要和之前那样，先把preorder数组排序得到中序，其实直接找到分割点就可以了，先序序列第一个节点一定是根，左子树所有结点都小于根节点，右子树所有结点都大于根节点,故可以使用lower_bound找到左右子树在当前先序序列中的划分点，递归处理左右子树。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def bstFromPreorder(self, preorder):
        """
        :type preorder: List[int]
        :rtype: TreeNode
        """
        if len(preorder)==0:
            return None
        root = TreeNode(preorder[0])
        j = 1
        for i in range(1,len(preorder)):
            if preorder[i]<preorder[0]:
                j+=1
            else:
                break
        root.left = self.bstFromPreorder(preorder[1:j])
        root.right = self.bstFromPreorder(preorder[j:])
        return root
```

