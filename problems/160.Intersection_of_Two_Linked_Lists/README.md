## 160.Intersection of Two Linked Lists

## 题目描述

编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表**：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

 

**示例 1：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```

 

**示例 2：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_2.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)

```
输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
```

 

**示例 3：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_3.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)

```
输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。
```

 

**注意：**

- 如果两个链表没有交点，返回 `null`.
- 在返回结果后，两个链表仍须保持原有的结构。
- 可假定整个链表结构中没有循环。
- 程序尽量满足 O(*n*) 时间复杂度，且仅用 O(*1*) 内存。



### 解答1

​	第一种就是暴力搜索，两个循环找出相交点。但是时间超时orz...

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        # 暴力搜索
        h1 = headA
        while h1:
            h2 = headB
            while h2:
                if h2 == h1:
                    return h2
                h2 = h2.next
            h1 = h1.next
        return None
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$



### 解答2

​	我们想一下这个结构，能不能找到两个点一起出发且速度一样，最后能一起走到相交点呢？答案是肯定的，我们只需要统计出两个链表的长度，然后一个指针从长的那个链表的头结点开始先走它们两个的长度差的距离，然后再一起往前遍历，如果有交点，那么肯定是一起到达。

```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def getIntersectionNode(self, headA, headB):
        """
        :type head1, head1: ListNode
        :rtype: ListNode
        """
        # 在相交的位置到最后部分是重合的，利用前面的长度差解题
        h1 = headA
        h2 = headB
        l1 = l2 = 0
        while h1:
            h1 = h1.next
            l1 += 1
        while h2:
            h2 = h2.next
            l2 += 1
        
        if l1 > l2:
            gap = l1-l2
            while gap:
                headA = headA.next
                gap-=1
            while headA and headB:
                if headA == headB:
                    return headA
                headA = headA.next
                headB = headB.next
            return
        else:
            gap = l2-l1
            while gap:
                headB = headB.next
                gap-=1
            while headA and headB:
                if headA == headB:
                    return headA
                headA = headA.next
                headB = headB.next
            return 
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

