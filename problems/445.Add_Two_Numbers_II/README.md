## 445.Add Two Numbers II

## 题目描述

给定两个非空链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储单个数字。将这两数相加会返回一个新的链表。

 

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

**进阶:**

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

**示例:**

```
输入: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出: 7 -> 8 -> 0 -> 7
```



### 解答

​	一开始想的是先反转，然后转化成第二题的解题思路，但是想到其实不用，在遍历的过程中直接用两个栈把节点的值存起来，然后按位相加时用头插法再建立一个新链表即可。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        stack1 = []
        stack2 = []
        while l1:
            stack1.append(l1.val)
            l1 = l1.next
        while l2:
            stack2.append(l2.val)
            l2 = l2.next
        dummy = ListNode(-1)
        flag = 0
        while stack1 or stack2:
            temp = 0
            if stack1:
                temp += stack1.pop(-1)
            if stack2:
                temp += stack2.pop(-1) 
            temp+=flag
            flag = temp//10
            temp %= 10
            p = ListNode(temp)
            p.next = dummy.next
            dummy.next = p
        if flag:
            p = ListNode(flag)
            p.next = dummy.next
            dummy.next = p
        return dummy.next
```

- 时间复杂度：$O(n)​$
- 空间复杂度：$O(n)$