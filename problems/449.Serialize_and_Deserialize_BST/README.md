## 449.Serialize and Deserialize BST

## 题目描述

序列化是将数据结构或对象转换为一系列位的过程，以便它可以存储在文件或内存缓冲区中，或通过网络连接链路传输，以便稍后在同一个或另一个计算机环境中重建。

设计一个算法来序列化和反序列化二叉搜索树。 对序列化/反序列化算法的工作方式没有限制。 您只需确保二叉搜索树可以序列化为字符串，并且可以将该字符串反序列化为最初的二叉搜索树。

编码的字符串应尽可能紧凑。

注意：不要使用类成员/全局/静态变量来存储状态。 你的序列化和反序列化算法应该是无状态的。



### 解答

​	这道题没什么好说的，只是建立二叉树的时候需要利用二叉搜索树的中序遍历为从小到大排列的性质，利用先序和中序建树。

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        def pre_order(res,root):
            if root==None:
                return res
            
            res.append(str(root.val))
            pre_order(res,root.left)
            pre_order(res,root.right)
            return res
        return ','.join(pre_order([],root))
        
        
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if len(data)==0:
            return None
        
        # 先序中序建立二叉树
        def buildTree(pre_o, in_o):
            if len(pre_o)==0:
                return None
            root = TreeNode(pre_o[0])
            s = in_o.index((pre_o[0]))
            root.left = buildTree(pre_o[1:s+1], in_o[:s])
            root.right = buildTree(pre_o[s+1:], in_o[s + 1:])
            return root
        pre_o = list(map(int,data.split(',')))
        in_o = sorted(pre_o)
        return buildTree(pre_o, in_o)

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

