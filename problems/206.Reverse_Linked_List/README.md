## 206.Isomorphic Strings

## 题目描述

反转一个单链表。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

**进阶:**
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？



### 解答1

​	迭代的方法就是使用头插法建立一个新的链表。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # 迭代,头插法
        dummy = ListNode(-1)
        while head!=None:
            temp = head
            head = head.next
            temp.next = dummy.next
            dummy.next = temp
            
        return dummy.next
```

- 时间复杂度：$O(n)​$
- 空间复杂度：$O(1)$ 

### 解答2

​	使用递归的方法解题。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        # 递归
        
        if head==None or head.next==None:
            return head
        prev = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return prev
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 	