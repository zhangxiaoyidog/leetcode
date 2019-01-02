## 082.Remove_Duplicates_from_Sorted_List_II

### 题目描述

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 *没有重复出现* 的数字。

**示例 1:**

```
输入: 1->2->3->3->4->4->5
输出: 1->2->5
```

**示例 2:**

```
输入: 1->1->1->2->3
输出: 2->3
```
### 解答

​	这道题关键也是在于把控好链表的四种指针(在第18题中我有提到)，使用这几个指针来控制链表的节点变换是很方便的，这道题的难点在于找到重复的串并删除和结尾的重复串的处理，处理重复和非重复情况的时候pre指针的变换也是不用的，这一点要注意。

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
            while nexts.val == cur.val:
               #  pre.next = nexts.next
                flag = 1
                nexts = nexts.next
                if nexts == None:
                    pre.next = None
                    return dummy.next
                
            if flag == 1:
                pre.next = nexts
            else:
                pre  = cur
            cur = nexts
            nexts = nexts.next
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 