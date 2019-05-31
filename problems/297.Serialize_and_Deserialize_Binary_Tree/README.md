## 297.Serialize and Deserialize Binary Tree

## 题目描述

序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**示例:** 

```
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

**提示:** 这与 LeetCode 目前使用的方式一致，详情请参阅 [LeetCode 序列化二叉树的格式](https://leetcode-cn.com/faq/#binary-tree)。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

**说明:** 不要使用类的成员 / 全局 / 静态变量来存储状态，你的序列化和反序列化算法应该是无状态的。



### 解答

​	这道题看似就是二叉树遍历和建立的问题，其实里面有不少细节需要注意，涉及到类型转换，特殊值处理等等问题，整个思路还是层次遍历和层次遍历的结果建树的思想，在层次遍历的时候需要注意把有些节点的空的孩子也要加进去，这点就很麻烦了，需要注意最后的那些None的处理，在建立树也就是反序列化的时候需要处理这些None值。

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
        if root==None:
            return '[]'
        
        res = '['
        vals = []
        nodes= [root]
        while nodes:
            node = nodes.pop(0)
            if node != None:
                vals.append(node.val)
                nodes.append(node.left)
                nodes.append(node.right)
            else:
                vals.append('null')
 
        while vals[-1]=='null':
            vals.pop(-1)
        
        for val in vals:
            res+=str(val)+','
        res = res[:-1]+']'
        return res

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if data=='[]' or data==None:
            return None
        data = data.replace("[","").replace("]","")
        data = data.split(',')
        root = TreeNode(int(data[0]))
        nodes = [root]
        idx = 1
        print(data)
        while nodes and idx<len(data):
            node = nodes[0]

            while node==None:
                nodes.pop(0)
                node = nodes[0]

            if data[idx]!='null':
                node.left = TreeNode(int(data[idx]))
            else:
                node.left = None
            nodes.append(node.left)
            if idx+1<len(data) and data[idx+1]!='null':
                node.right = TreeNode(int(data[idx+1]))
            else:
                node.right = None
            nodes.append(node.right)
            idx+=2
            nodes.pop(0)
        return root

# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.deserialize(codec.serialize(root))
```

