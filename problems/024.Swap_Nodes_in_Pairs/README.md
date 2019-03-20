## 024.Swap Nodes in Pairs

### 题目描述

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**示例:**

```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

**说明:**

- 你的算法只能使用常数的额外空间。
- **你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。



### 解答1

​	这道题一开始我的思路就是在遍历的过程中去设置两个指针，然后做一些交换的操作，也就是常规做法，详见下图。

![](https://note.youdao.com/yws/api/personal/file/WEBb2e52b14748a889ad1b0efd9bb4f6a9c?method=download&shareKey=c5e5ec315b868279e8bcf9bd49313472)



```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None:
            return []
        dummy = ListNode(0)
        dummy.next = head
        head = dummy
        l = dummy.next
        r = l.next
        
        while l!=None and r!=None:
            l.next = r.next
            r.next = l
            head.next = r
            head = l
            
            l = l.next
            if l!= None:
                r = l.next
        return dummy.next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

### 解答2

​	在看disscuss的时候发现了递归求解的方法，非常简洁，于是借鉴了其中的思路。

```python
class Solution:
    def swapPairs(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        if head == None or head.next == None:
            return head
        
        #递归求解
        l_next = head.next
        head.next = self.swapPairs(l_next.next)
        l_next.next = head
        return l_next
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$