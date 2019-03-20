## 147.Insertion Sort List

## 题目描述

对链表进行插入排序。

![img](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)
插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。
每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。

 

**插入排序算法：**

1. 插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
2. 每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
3. 重复直到所有输入数据插入完为止。

 

**示例 1：**

```
输入: 4->2->1->3
输出: 1->2->3->4
```

**示例 2：**

```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```



### 解答

​	这道题目我的做法也是常规做法，心就是新建一个链表头，把原来的节点一个个插进去，过程也是比较简单。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def insertionSortList(self, head: ListNode) -> ListNode:
        
        if head==None or head.next==None:
            return head
        # 新建一个链表，原链表插进去
        dummy = ListNode(-1)
        
        while head!=None:
            node = dummy
            rear = head.next
            while node.next!=None and node.next.val<head.val:
                node = node.next
            head.next = node.next
            node.next = head
            head = rear
        return dummy.next
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$