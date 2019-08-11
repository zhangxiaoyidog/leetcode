## 148.Sort List

## 题目描述

在 *O*(*n* log *n*) 时间复杂度和常数级空间复杂度下，对链表进行排序。

**示例 1:**

```
输入: 4->2->1->3
输出: 1->2->3->4
```

**示例 2:**

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```



### 解答

​	看到O(nlogn)的时间复杂度，可以选择使用归并排序来做，但是链表没法使用指针从后往前，那就用merge sort的方式，也就是递归地把链表分成两段，然后不停合并的过程，在分割的过程总会变成只有一个节点的两个链表的情况，合并就变成有序的了，这样就相当于做过的合并两个有序链表的题目。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        # 看到O(nlogn)的时间复杂度，可以选择使用归并排序来做
        # 但是链表没法使用指针从后往前，只能用merge sort的方式
        
        if head==None or head.next==None:
            return head
        slow = head
        fast = head
        while fast!=None and fast.next!=None:
            pre = slow
            slow = slow.next
            fast = fast.next.next
        # 分成两段
        pre.next = None
        l1 = self.sortList(head)
        l2 = self.sortList(slow)
        
        return self.merge(l1,l2)
    def merge(self,l1,l2):
        # 合并两个排序链表
        dummy = ListNode(-1)
        head1 = dummy
        while l1 and l2:
            if l1.val<l2.val:
                head1.next = l1
                l1 = l1.next
            else:
                head1.next = l2
                l2= l2.next
            head1 = head1.next
        if l1:
            head1.next = l1
        if l2:
            head1.next = l2

        return dummy.next
```

- 时间复杂度：$O(nlog(n))$
- 空间复杂度：$O(1)$



### 解答2

​	最近看到有面经上说有公司在面试中问到这道题，但是要求不能只交换节点的值，而是要交换节点，所以这里记录一下，思想是用两个新链表存储左边和右边部分，最后在合并，但是提交超时了。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        # 用快排的思想做
        if head==None or head.next==None:
            return head
        pivot = head
        # 用两个新建链表分别存储左边和右边
        left_dummy = ListNode(-1)
        right_dummy = ListNode(-1)
        left, right = left_dummy, right_dummy
        cur = head.next
        while cur:
            if cur.val<pivot.val:
                left.next = cur
                left = left.next
            else:
                right.next = cur
                right = right.next
            cur = cur.next
        
        left.next = None
        right.next = None
        left = self.sortList(left_dummy.next)
        right = self.sortList(right_dummy.next)
        
        # 合并
        if left:
            res = left
            while left.next:
                left = left.next
            left.next = pivot
            pivot.next = right
            return res
        else:
            pivot.next = right
            return pivot
```

### 解答3

​	快排的话也可以只交换节点的值，但是这里比较巧妙，我们只需要两个指针p和q，这两个指针均往next方向移动，移动的过程中保持p之前的key都小于选定的key，q是一直往前移动，当q的值小于pivot的时候，把p往前移一步，交换p和q的值，这样就可以保证p和q之间的key都大于选定的key，那么当q走到末尾的时候便完成了一次分界点的寻找。但是很遗憾也提交超时了orz……

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        # 用快排的思想做
        if head==None or head.next==None:
            return head
        self.QuickSort(head,None)
        return head
    
    def QuickSort(self,pBeign,pEnd):
        if pBeign!=pEnd:
            p = self.partition(pBeign,pEnd)
            self.QuickSort(pBeign,p)
            self.QuickSort(p.next,None)
        
    def partition(self, begin, end):
        # 只交换值
        if begin==None or begin.next==None:
            return begin
        pivot = begin.val
        p = begin
        q = p.next
        while q!=end:
            if q.val<pivot:
                p = p.next
                p.val,q.val = q.val,p.val
            q = q.next
        p.val, begin.val = begin.val, p.val
        return p
```

