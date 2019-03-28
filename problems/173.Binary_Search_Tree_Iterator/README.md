## 173.Binary Search Tree Iterator

## 题目描述

实现一个二叉搜索树迭代器。你将使用二叉搜索树的根节点初始化迭代器。

调用 `next()` 将返回二叉搜索树中的下一个最小的数。

 

**示例：**

**![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/25/bst-tree.png)**

```
BSTIterator iterator = new BSTIterator(root);
iterator.next();    // 返回 3
iterator.next();    // 返回 7
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 9
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 15
iterator.hasNext(); // 返回 true
iterator.next();    // 返回 20
iterator.hasNext(); // 返回 false
```

 

**提示：**

- `next()` 和 `hasNext()` 操作的时间复杂度是 O(1)，并使用 O(*h*) 内存，其中 *h* 是树的高度。
- 你可以假设 `next()` 调用总是有效的，也就是说，当调用 `next()` 时，BST 中至少存在一个下一个最小的数。



### 解答

​	这道题我们需要定义一个栈来实现这三个功能，在next()方法中，栈中每轮压入某个节点和它的右孩子、左孩子，并把它的状态设置为0，那么这样在弹出时状态为0的那个必然是最小的。

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class BSTIterator:

    def __init__(self, root: TreeNode):
        self.stack = []
        if root:
            self.stack.append((1,root))
        
    def next(self) -> int:
        """
        @return the next smallest number
        """
        stack = self.stack
        while stack:
            this_node = stack.pop()
            if not this_node[1]:
                continue
            if this_node[0]==0:
                return this_node[1].val
            else:
                if this_node[1].right:
                    stack.append((1,this_node[1].right))
                stack.append((0,this_node[1]))
                if this_node[1].left:
                    stack.append((1,this_node[1].left))

    def hasNext(self) -> bool:
        """
        @return whether we have a next smallest number
        """
        if len(self.stack)>0:
            return True
        else:
            return False


# Your BSTIterator object will be instantiated and called as such:
# obj = BSTIterator(root)
# param_1 = obj.next()
# param_2 = obj.hasNext()
```

