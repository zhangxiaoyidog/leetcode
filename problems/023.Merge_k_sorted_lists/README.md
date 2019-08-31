## 023.Merge k Sorted Lists

### 题目描述

合并 *k* 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

**示例:**

```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```



###解答1

​	这道题我的思路也就是比较简单直接的，提交之后时间复杂度也没有很高，大致做法就是先把所有的节点的值放在一个列表中，排序后再新建一个链表，返回即可。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        # 将所有的节点的值放在一个列表中，排序后再新建一个链表
        
        nodes = []
        new_head = cur = ListNode(0)
        
        for l in lists:
            while l:
                nodes.append(l.val)
                l = l.next
        nodes.sort()
        for node in nodes:
            new_n = ListNode(0)
            cur.next = new_n
            cur = cur.next
            cur.val = node
        return new_head.next
```

- 时间复杂度：$O(nlogn)$
- 空间复杂度：$O(n)$



### 解答2

​	可以使用分治法的思想，不断两两合并，最后返回第一个即可。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        # 分治法
        hop = 1
        total = len(lists)
        while hop<total:
            print(total)
            for i in range(0,total-hop,hop*2):
                lists[i] = self.mergeTwoLists(lists[i], lists[i+hop])
            hop *= 2
        return lists[0] if total > 0 else None
        
    def mergeTwoLists(self, l1, l2):
        print(111)
        dummy_node = ListNode(-1)
        l_temp = dummy_node

        while l1 != None and l2 != None:
            if l1.val <= l2.val:
                l_temp.next = l1
                l1 = l1.next
            else:
                l_temp.next = l2
                l2 = l2.next
            l_temp = l_temp.next

        if l1 != None:
            l_temp.next = l1
        if l2 != None:
            l_temp.next = l2
            
        return dummy_node.next
```

