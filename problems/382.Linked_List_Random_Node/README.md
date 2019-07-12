## 382.Linked List Random Node

### 题目描述

给定一个单链表，随机选择链表的一个节点，并返回相应的节点值。保证每个节点被选的概率一样。

**进阶:**
如果链表十分大且长度未知，如何解决这个问题？你能否使用常数级空间复杂度实现？

**示例:**

```
// 初始化一个单链表 [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);

// getRandom()方法应随机返回1,2,3中的一个，保证每个元素被返回的概率相等。
solution.getRandom();
```



### 解答1

​	首先遍历链表得到长度，然后使用random方法得到这个长度以内的一个随机数，然后移动到这个位置返回即可。

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:

    def __init__(self, head: ListNode):
        """
        @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node.
        """
        p = head
        self.l = 0
        self.h = head
        while p:
            p = p.next
            self.l+=1
            
        
    def getRandom(self) -> int:
        """
        Returns a random node's value.
        """
        h = self.h
        r = random.randint(1,self.l)-1
        while r:
            h = h.next
            r-=1
        return h.val
            

# Your Solution object will be instantiated and called as such:
# obj = Solution(head)
# param_1 = obj.getRandom()
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	假如我们不能提前知道链表长度，也就是长度超过了表示方法，那么这里我们直接采取另一种思路，即著名的水塘抽样，首先我们取到第一个数（暂时取的最后要不要还不一定呢），然后对第二个数以1/2的概率来确定是否用第二个数来替换他，然后对第二个数以1/3的概率来确定是否用第三个数来替换他。一直这样下去直到第n个数。经过上面的这个过程我们发现每个数取到的概率都变成了（1/n）。

```
证明:
对第i个元素他被选到的概率为:他被选到的概率*后面未被替换的概率
1/i*(i/i+1)*……*(n-1/n) = 1/n
为什么一开始被选到概率为1/i？
因为前面的情况可以不考虑，只考虑第i个位置，就是1/i
```



```python
from random import randint
class Solution:

    def __init__(self, head: ListNode):
        """
        @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node.
        """
        self.list = head
        

    def getRandom(self) -> int:
        """
        Returns a random node's value.
        """
        res = None
        node = self.list
        count = 0
        while node:
            if not randint(0, count):
                res = node.val
            count += 1
            node = node.next
        return res
```

