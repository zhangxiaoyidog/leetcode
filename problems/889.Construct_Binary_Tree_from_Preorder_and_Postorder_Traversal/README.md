## 889.Construct Binary Tree from Inorder and Postorder Traversal

## 题目描述

返回与给定的前序和后序遍历匹配的任何二叉树。

 pre 和 post 遍历中的值是不同的正整数。

 

**示例：**

```
输入：pre = [1,2,4,5,3,6,7], post = [4,5,2,6,7,3,1]
输出：[1,2,3,4,5,6,7]
```



提示：

+ 1 <= pre.length == post.length <= 30
+ pre[] 和 post[] 都是 1, 2, ..., pre.length 的排列
+ 每个输入保证至少有一个答案。如果有多个答案，可以返回其中一个。



### 解答

​	还是和105 106题一样的套路，找分界点递归，不过这个特殊一点，需要用pre的第二个节点去从post中找。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def constructFromPrePost(self, pre: List[int], post: List[int]) -> TreeNode:
        if len(pre) == 0 or len(post) == 0:
            return None
        
        root = TreeNode(pre[0])
        
        if len(pre)==1:
            return root
        divided_node = post.index(pre[1])
        root.left = self.constructFromPrePost(pre[1:divided_node+2],post[:divided_node+1])
        root.right = self.constructFromPrePost(pre[divided_node+2:],post[divided_node+1:-1])
        
        return root
```

