## 142.Linked List Cycle II

## 题目描述

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 `null`。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

**说明：**不允许修改给定的链表。

 

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

**示例 2：**

```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

**示例 3：**

```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**进阶：**
你是否可以不用额外空间解决此题？



### 解答1

​	和上一道题一样，使用额外空间，这里我是用的是字典，假如有环，在第一次遍历到就会加入字典，一开始我以为要返回位置，所以使用字典存储位置信息，其实不用，返回节点就行，否则返回None。

```python
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        d = {}
        i = 0
        while head!= None:
            if head not in d:
                d[head] = i
                i+=1
            else:
                return head
            head = head.next
        return None
```

- 时间复杂度：$O(n)​$
- 空间复杂度：$O(n)$



### 解答2

​	第二种解法也是使用快慢指针，假如有环，在相遇的时候，假如slow走了x步，则fast走了2x步，slow走的是起点到环开始的点的距离s1加上环开始点到相遇点的距离s2，而fast走的是s1加s2再加上相遇点到环起点的距离s3，最后再加上环起点到相遇点的距离s2，发现了没有，其实s3等于s1，这里画图的话会更清晰，那么我们如何找到起点呢，bingo！这里再用一个指针从head开始，fast也开始走，每次都只走一步，等到相遇的时候，就刚好走到环的起点了，因为s1等于s3。

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def detectCycle(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        # 快慢指针
        fast_node = head
        slow_node = head
        
        while fast_node!=None and fast_node.next!=None:
            fast_node = fast_node.next.next
            slow_node = slow_node.next
            if fast_node==slow_node:
                q = head
                while q!=fast_node:
                    q = q.next
                    fast_node = fast_node.next
                return q
        return None
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

