## 061.Rotate_List

### 题目描述

给定一个链表，旋转链表，将链表每个节点向右移动 *k* 个位置，其中 *k* 是非负数。

**示例 1:**

```
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```

**示例 2:**

```
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```

### 解答

​	这道题其实很简单，我的思路是先得到链表的length，也就是找到最后的节点，然后这里要做一个取余的操作，也就是k%length，因为向右移动length+k和k个的效果是一样的，然后观察一下，向右移动k个，也就是把后k个节点移到最前面而已，所以找到倒数第k个节点，把它做为head，它之前的节点都顺序链接到最后面即可。关键还是之前提到的链表中的四大指针的一个灵活运用。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def rotateRight(self, head, k):
        """
        :type head: ListNode
        :type k: int
        :rtype: ListNode
        """
        if head == None or k == 0:
            return head
        length = 1
        temp_last = head
        # 先求出length
        while temp_last.next != None:
            temp_last = temp_last.next
            length += 1
        # 取余操作
        if k % length == 0:
            return head
        k1 = length - k % length
        dummy = ListNode(-1)
        dummy.next = head
        pre = dummy
        cur = head
        while k1 > 0:
            pre = pre.next
            cur = cur.next
            k1 -= 1
        temp_last.next = head
        pre.next = None
        return cur        
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 