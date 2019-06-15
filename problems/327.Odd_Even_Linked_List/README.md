## 327.Odd Even Linked List

## 题目描述

给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

**示例 1:**

```
输入: 1->2->3->4->5->NULL
输出: 1->3->5->2->4->NULL
```

**示例 2:**

```
输入: 2->1->3->5->6->4->7->NULL 
输出: 2->3->6->7->1->5->4->NULL
```

**说明:**

+ 应当保持奇数节点和偶数节点的相对顺序。
+ 链表的第一个节点视为奇数节点，第二个节点视为偶数节点，以此类推。



### 解答

​	使用尾插法将奇数节点和偶数节点新建两个链表，最后把两个链表首尾连起来。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        # 尾插法新建两个新链表
        if head==None or head.next==None:
            return head
        dummy_odd = ListNode(-1)
        odd = dummy_odd
        dummy_even = ListNode(-1)       
        even = dummy_even
        cur = head
        flag = 1
        while cur:
            # 奇数节点
            head = cur.next
            if flag%2:
                odd.next = cur
                odd = odd.next
                cur.next = None
            else:
                even.next = cur
                even = even.next
                cur.next = None
            flag+=1
            cur = head
        # merge
        odd.next = dummy_even.next
        return dummy_odd.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 