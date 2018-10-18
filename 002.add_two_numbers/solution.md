# 001. Add Two Nunbers

## 题目描述

给定两个**非空**链表来表示两个非负整数。位数按照**逆序**方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

**示例:**

```java
输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

## 解答

​	这个问题就是简单的链表节点相加的问题，对应的节点值相加，然后考虑进位的问题，不断向前递进直到两个链表都为空。考虑清楚后实现起来是比较简单的，但是编程过程中要考虑很多小细节，这一点要注意！！！

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode node = new ListNode(0);
        
        ListNode a = l1;
        ListNode b = l2;
        ListNode c = node;
        int flag = 0;
        while(a!= null || b!=null){
            int m = 0;
            int n = 0;
            if (a !=null){
                m = a.val;
            }
            if (b !=null){
                n = b.val;
            }
            //c.val = a.val + b.val;
            int curr = flag +  m + n;
            flag = curr / 10;
            c.val = curr % 10;
            if(a!=null) a = a.next;
            if(b!=null) b = b.next;
            if (a!= null || b!=null){
                c.next = new ListNode(0);
                c = c.next;
            }
            
        }
        if (flag>0){
            c.next = new ListNode(flag);
        }
        return node;
    }
}
```

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        node = ListNode(0)
        la = l1
        lb = l2
        c = node
        flag = 0
        while la!= None or lb !=None:
            m = 0
            n = 0
            if la!=None:
                m = la.val
            if lb!=None:
                n = lb.val
            curr = flag + m +n
            flag = curr // 10
            c.val = curr % 10
            # 全为and，如果都为真，则返回最后一个变量值；如果为假，则返回第一个假值
            la = la and la.next
            lb = lb and lb.next
            if (la!= None or lb!=None):
                c.next = ListNode(0);
                c = c.next;
        if (flag>0):
            c.next = ListNode(flag)
            
        return node
```



复杂度分析：

- 时间复杂度：$O(max(m,n))$
- 空间复杂度：$O(max(m,n))$
