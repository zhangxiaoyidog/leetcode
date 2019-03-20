## 143.Reorder List

## 题目描述

给定一个单链表 *L*：*L*0→*L*1→…→*L**n*-1→*L*n ，
将其重新排列后变为： *L*0→*L**n*→*L*1→*L**n*-1→*L*2→*L**n*-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

**示例 1:**

```
给定链表 1->2->3->4, 重新排列为 1->4->2->3.
```

**示例 2:**

```
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```



### 解答

​	这道题我能想到的是一个比较麻烦的解法，首先使用快慢指针法找到中间点，然后用头插法把后半段链表反转，反转之后重新插入到前半段中。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reorderList(self, head: ListNode) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        if head==None or head.next==None or head.next.next==None:
            return
        dummy = ListNode(-1)
        dummy.next = head
    
        # 快慢指针找到中间点
        slow = head
        fast = head
        while fast!=None and fast.next!=None and fast.next.next:
            slow = slow.next
            fast = fast.next.next
        
        # 后半段链表翻转,头插法
        dummy1 = ListNode(-1)
        pre = slow
        slow = slow.next
        pre.next = None
        
        # print(slow.val)
        
        while slow!=None:
            temp = slow
            slow = slow.next
            temp.next = dummy1.next
            dummy1.next = temp
        #print(temp.val)
        # 重新插入到原链表
        head2 = dummy1.next
        cur = head    
        while cur!=None and head2:
            
            insert_node = head2
            head2 = head2.next
            next_cur = cur.next
            insert_node.next = cur.next
            cur.next = insert_node
            
            cur = next_cur
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

