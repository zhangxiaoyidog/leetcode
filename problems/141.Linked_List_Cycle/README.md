## 141.Linked List Cycle

## 题目描述

给定一个链表，判断链表中是否有环。

为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。

 

**示例 1：**

```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist.png)

**示例 2：**

```
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test2.png)

**示例 3：**

```
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/07/circularlinkedlist_test3.png)

 

**进阶：**

你能用 *O(1)*（即，常量）内存解决此问题吗？



### 解答

​	第一种解法就是使用额外空间，可以使用字典、列表、集合来存储遍历过的节点，假如有环是可以最后是可以在集合中找到的，否则无环。

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        s = set()
        
        while head!=None:
            if head not in s:
                s.add(head)
            else:
                return True
            head = head.next
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$



### 解答2

​	第二种解答是使用快慢指针，fast指针每次走两步，slow指针每次只走一步，假如有环肯定会相遇，否则不会。

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        fast_node = head
        slow_node = head
        
        while fast_node!=None and fast_node.next!=None:
            fast_node = fast_node.next.next
            slow_node = slow_node.next
            if fast_node==slow_node:
                return True
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$