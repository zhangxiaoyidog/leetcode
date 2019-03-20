## 092.Reverse linked list II

## 题目描述

反转从位置 *m* 到 *n* 的链表。请使用一趟扫描完成反转。

**说明:**
1 ≤ *m* ≤ *n* ≤ 链表长度。

**示例:**

```
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```



### 解答1

​	首先想到了之前做的一道题，先找到要反转的第一个节点，然后在遍历的过程中使用头插法插入到一个新链表中，最后把新链表再加入到原链表中。具体的细节看代码，还是使用之前的套路－四大指针。

```python
class Solution:
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if n - m < 1:
            return head
        # 1 ≤ m ≤ n ≤ 链表长度。
        dummy = ListNode(-1)
        dummy.next = head
        cur = dummy
        
        dummy2 = ListNode(-1)
        i = 1
        # 找到要反转的第一个节点
        while i < m :
            i+=1
            cur = cur.next
            head = head.next
        tail = head
        # 然后头插到另一个链表上
        while i <= n:
            i+=1
            head = head.next
            cur.next.next = dummy2.next
            dummy2.next = cur.next
            cur.next = head
        
        # 加入到原链表
        tail.next = cur.next
        cur.next = dummy2.next
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答２

​	第二种解法就是直接在原链表上修改咯，用三个指针来解决这个问题，具体的细节看代码即可，也是比较简单的。

```python
class Solution:
    def reverseBetween(self, head, m, n):
        """
        :type head: ListNode
        :type m: int
        :type n: int
        :rtype: ListNode
        """
        if n - m < 1:
            return head
        # 1 ≤ m ≤ n ≤ 链表长度。
        dummy = ListNode(-1)
        dummy.next = head
        
        pre = dummy
        
        for i in range(m-1):
            pre = pre.next
        cur = pre.next
        nexts = cur.next
        
        while nexts and m<n:
            cur.next = nexts.next
            nexts.next = pre.next
            pre.next = nexts
            nexts = cur.next
            m+=1
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

