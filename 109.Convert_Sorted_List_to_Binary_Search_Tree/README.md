## 109.Convert Sorted List to Binary Search Tree

## 题目描述

给定一个单链表，其中的元素按升序排序，将其转换为高度平衡的二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1。

**示例:**

```
给定的有序链表： [-10, -3, 0, 5, 9],

一个可能的答案是：[0, -3, 9, -10, null, 5], 它可以表示下面这个高度平衡二叉搜索树：

      0
     / \
   -3   9
   /   /
 -10  5
```

### 解答

​	这道题跟上面一道题很相似，但是这里怎么找中间点是一个难点，有一个比较笨的方法是先把链表转化成list，然后再去生成二叉搜索树。然而这样做就太没意思了，所以我们还是使用链表的常规方法，把握好它的四大指针，这里使用了三个指针pre，slow，fast。在一次递归中pre最后指向此时的左子树全部节点的最后一个，slow是根节点，fast用来判断是否找到了中心点。这里找中心点的一个技巧就是pre、slow、fast同时往后移，slow往后移动一步，fast往后两步，这样fast移到最后的时候，slow正好在最中间。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def sortedListToBST(self, head):
        """
        :type head: ListNode
        :rtype: TreeNode
        """
        if head == None:
            return None
        if head.next == None:
            return TreeNode(head.val)
        dummy = TreeNode(-1)
        # 使用三个指针,pre指向左子树全部节点的最后一个
        # slow是根节点,fast用来判断是否找到了中心点
        dummy.next = head
        pre = dummy
        slow = head
        fast = head
        while fast!=None and fast.next!=None:
            pre = slow
            slow = slow.next
            fast = fast.next.next
        
        root = TreeNode(slow.val)
        pre.next = None
        root.left = self.sortedListToBST(dummy.next)
        root.right = self.sortedListToBST(slow.next)
        
        return root
```

