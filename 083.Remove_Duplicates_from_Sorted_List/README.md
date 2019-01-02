## 083.Remove_Duplicates_from_Sorted_List

### 题目描述

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

**示例 1:**

```
输入: 1->1->2
输出: 1->2
```

**示例 2:**

```
输入: 1->1->2->3->3
输出: 1->2->3
```

### 解答

​	这道题跟上一道题很相似，这道题其实更为简单，重复的情况直接处理就行了，直接上代码。



```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteDuplicates(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None or head.next == None:
            return head
        
        dummy = ListNode(-1)
        dummy.next = head
        
        pre = dummy
        cur = dummy.next
        nexts = cur.next
        while nexts!= None:
            flag = 0
            if nexts.val == cur.val:
               #  pre.next = nexts.next
                nexts = nexts.next
                if nexts == None:
                    cur.next = None
                    return dummy.next
            else:
                pre = cur
                cur = nexts
                pre.next = cur
                nexts = nexts.next
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 