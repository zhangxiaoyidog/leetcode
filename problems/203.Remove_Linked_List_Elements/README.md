## 203.Remove Linked List Elements

## 题目描述

删除链表中等于给定值 **val** 的所有节点。

**示例:**

```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```



### 解答

​	这道题比较简单，也是使用四大指针去做就好了，在往后遍历的过程找到目标节点删除就可以了。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        pre = dummy
        while head!=None:
            if head.val==val:
                pre.next = head.next
                head = pre.next
            else:
                head = head.next
                pre = pre.next
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 