## 095.**Unique Binary Search Trees II**

## 题目描述

给定一个整数 *n*，生成所有由 1 ... *n* 为节点所组成的**二叉搜索树**。

**示例:**

```
输入: 3
输出:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释:
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```



### 解答

​	这一类题目看到就要想到使用递归算法去解决，二叉搜索树的特点就是左子树的值比根节点的值小，右子树的值都比根节点的值大。所以递归的时候是遍历所有的n，也就是每个数字都可能作为根节点，那么对于每一个值i，左子树的的值就是[min,i-1]，右子树的值为[i+1,max]，然后再去递归左子树和右子树，最后返回的是一个树的root的list，其实递归的过程和上一题遍历有一些相似之处，这里也可以看出来这一类递归和之前做过的回溯的一些区别。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def generateTrees(self, n):
        """
        :type n: int
        :rtype: List[TreeNode]
        """
        res = self.recursion_generate(1,n)
        return res
    
    
    def recursion_generate(self,min_val,max_val):
        """
        使用递归来处理
        """
        # res中存的是树的root
        res = []
        if min_val>max_val:
            return res
        
        for i in range(min_val,max_val+1):
            left_res = self.recursion_generate(min_val,i-1)
            right_res = self.recursion_generate(i+1,max_val)
            # 左子树和右子树都为空
            if len(left_res) == 0 and len(right_res) == 0:
                root = TreeNode(i)
                res.append(root)
            # 左子树为空
            elif len(left_res) == 0:
                for right_root in right_res:
                    root = TreeNode(i)
                    root.right = right_root
                    res.append(root)
            # 右子树为空
            elif len(right_res) == 0:
                for left_root in left_res:
                    root = TreeNode(i)
                    root.left = left_root
                    res.append(root)
            else:
                for left_root in left_res:
                    for right_root in right_res:
                        root = TreeNode(i)
                        root.left = left_root
                        root.right = right_root
                        res.append(root)
        return res
```

