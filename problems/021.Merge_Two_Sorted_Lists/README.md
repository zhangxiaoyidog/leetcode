## 021.Merge Two Sorted Lists

### 题目描述

将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

### 解答

​	这道题很简单，关键也是在于把控好链表的四种指针(在第19题中我有提到)，之前第二题的编程思想可以直接拿过来用，这道题比第2题还要简单不少，所以这里不再赘述，可以直接看代码。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        
        dummy_node = ListNode(-1)
        l_temp = dummy_node
        
        while l1 != None and l2 != None:
            if l1.val <= l2.val:
                l_temp.next = l1
                l1 = l1.next
            else:
                l_temp.next = l2
                l2 = l2.next
            l_temp = l_temp.next
        
        if l1 != None:
            l_temp.next = l1
        if l2 != None:
            l_temp.next = l2
        return dummy_node.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 