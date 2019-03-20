## 148.Sort List

## 题目描述

在 *O*(*n* log *n*) 时间复杂度和常数级空间复杂度下，对链表进行排序。

**示例 1:**

```
输入: 4->2->1->3
输出: 1->2->3->4
```

**示例 2:**

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```



### 解答

​	看到O(nlogn)的时间复杂度，可以选择使用归并排序来做，但是链表没法使用指针从后往前，那就用merge sort的方式，也就是递归地把链表分成两段，然后不停合并的过程，在分割的过程总会变成只有一个节点的两个链表的情况，合并就变成有序的了，这样就相当于做过的合并两个有序链表的题目。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        # 看到O(nlogn)的时间复杂度，可以选择使用归并排序来做
        # 但是链表没法使用指针从后往前，只能用merge sort的方式
        
        if head==None or head.next==None:
            return head
        slow = head
        fast = head
        while fast!=None and fast.next!=None:
            pre = slow
            slow = slow.next
            fast = fast.next.next
        # 分成两段
        pre.next = None
        l1 = self.sortList(head)
        l2 = self.sortList(slow)
        
        return self.merge(l1,l2)
    def merge(self,l1,l2):
        # 合并两个排序链表
        dummy = ListNode(-1)
        head1 = dummy
        while l1 and l2:
            if l1.val<l2.val:
                head1.next = l1
                l1 = l1.next
            else:
                head1.next = l2
                l2= l2.next
            head1 = head1.next
        if l1:
            head1.next = l1
        if l2:
            head1.next = l2

        return dummy.next
```

- 时间复杂度：$O(nlog(n))$
- 空间复杂度：$O(1)$

