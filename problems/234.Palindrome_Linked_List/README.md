## 234.Palindrome Linked List

## 题目描述

请判断一个链表是否为回文链表。

**示例 1:**

```
输入: 1->2
输出: false
```

**示例 2:**

```
输入: 1->2->2->1
输出: true
```

**进阶：**
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？



### 解答

​	比较简单的思路是利用头插法再新建一个链表，判断每个位置的值是否相同即可，这里假如不使用额外空间怎么做呢？其实也不算麻烦，首先使用快慢指针找到后半段然后把后半段逆转成另一个链表，最后判断即可。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        if head==None:
            return True
        
        # 首先使用快慢指针找到后半段
        fast = head
        slow = head
        while fast!=None and fast.next!=None:
            slow = slow.next
            fast = fast.next.next
        print(slow.val)
        # 判断链表长度为奇数的情况
        if fast!=None:
            slow = slow.next
        dummy = ListNode(-1)
        
        # 后半段新建链表
        while slow!=None:
            temp = slow.next
            slow.next = dummy.next
            dummy.next = slow
            slow =temp
        
        slow = dummy.next
        while slow and head:
            if slow.val!=head.val:
                return False
            slow = slow.next
            head = head.next
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 