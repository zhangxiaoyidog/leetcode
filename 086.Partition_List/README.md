## 086.Partition_List

### 题目描述

给定一个链表和一个特定值 *x*，对链表进行分隔，使得所有小于 *x* 的节点都在大于或等于 *x* 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

**示例:**

```
输入: head = 1->4->3->2->5->2, x = 3
输出: 1->2->2->4->3->5
```



### 解答

​	对于这一类问题还是一样的套路，把握好四种指针，剩下的就是一些常见的解决方法，这道题一个比较方便的解答是遍历链表，把大于等于target的节点田家达另一个新链表中，其余的留下，最后合并就完事了，也有其他的解法，不过这个应该是比较直观的一种。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def partition(self, head, x):
        """
        :type head: ListNode
        :type x: int
        :rtype: ListNode
        """
        
        dummy = ListNode(-1)
        dummy.next = head
        pre = dummy
        
        dummy2 = ListNode(-1)
        pre2 = dummy2
        
        while head!=None:
            if head.val<x:
                pre = pre.next
                head = head.next
            else:
                pre.next = head.next
                head.next = pre2.next
                pre2.next = head
                pre2 = pre2.next
                head = pre.next
        pre.next = dummy2.next
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 