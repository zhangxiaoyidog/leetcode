## 019.Remove Nth Node From End of List

### 题目描述

给定一个链表，删除链表的倒数第 *n* 个节点，并且返回链表的头结点。

**示例：**

```
给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
```

**说明：**

给定的 *n* 保证是有效的。

**进阶：**

你能尝试使用一趟扫描实现吗？



### 解答1

​	这道题的第一种解法就是先得到链表的长度length，然后把倒数第n个节点转化成正数第length-n+1个节点，然后遍历找到并删除这个节点就好了。要注意的地方就是只有一个节点的这种情况，所以需要额外定义一个节点来处理这种情况。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        # 先用一个指针去得到链表长度
        l1 = head
        length = 0
        while l1 != None:
            l1 = l1.next
            length+=1     
        length-=n

        l2 = ListNode(0)
        l2.next = head
        l1 = l2
        for i in range(length):
            l1 = l1.next
        l1.next = l1.next.next
        return l2.next
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	上面的那种解法的时间复杂度虽然为$O(n)$，但是仍然扫描了两遍链表，能否想办法只扫描一遍？答案是肯定的，解决方法就是使用两个指针，两个指针之间的间隔就是倒数第n个节点与最后节点之间的间隔，同时向后扫描，当第一个指针到达最后的节点的时候，第二个则处于要删除的节点位置，细节需要注意同上。

​	链表题目中有四大指针，控制好这四大指针，一般题目都能够很快的求解出来:

```java
ListNode dummy = new ListNode(-1);
ListNode pre = dummy;
ListNode cur = dummy.next;
ListNode next = cur.next;
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        node = ListNode(0)
        node.next = head
        l1 = node
        l2 = node
        for i in range(n+1):
            l2 = l2.next

        while l2!=None:
            l1 = l1.next
            l2 = l2.next
        l1.next = l1.next.next
        return node.next
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

