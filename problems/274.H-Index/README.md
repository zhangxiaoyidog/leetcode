## 274.H-Index

## 题目描述

给定一位研究者论文被引用次数的数组（被引用次数是非负整数）。编写一个方法，计算出研究者的 *h* 指数。

[h 指数的定义](https://baike.baidu.com/item/h-index/3991452?fr=aladdin): “h 代表“高引用次数”（high citations），一名科研人员的 h 指数是指他（她）的 （N 篇论文中）**至多**有 h 篇论文分别被引用了**至少** h 次。（其余的 *N - h* 篇论文每篇被引用次数**不多于** *h* 次。）”

 

**示例:**

```
输入: citations = [3,0,6,1,5]
输出: 3 
解释: 给定数组表示研究者总共有 5 篇论文，每篇论文相应的被引用了 3, 0, 6, 1, 5 次。
     由于研究者有 3 篇论文每篇至少被引用了 3 次，其余两篇论文每篇被引用不多于 3 次，所以她的 h 指数是 3。
```

 

**说明:** 如果 *h* 有多种可能的值，*h* 指数是其中最大的那个。



### 解答

​	这道题的答案和在列表中，也就是可以看成是查找问题，所以将列表排序后可以转化成二分查找的问题来解决，根据题意：找的是某个点，在**满足这个点的值** >= **它和它右侧的点个数之的**情况下，右侧和就是当前的h指数。如果已经有h指数了，就可以试着往左找，因为越左cnt越大，h指数也越大，所以左侧可能存在更大的h值，如果目前还没有h指数，就只能试着缩小cnt，往右找。

```python
class Solution:
    def hIndex(self, citations: List[int]) -> int:
        if len(citations)==0:
            return 0
        citations.sort()
        l = 0
        r = len(citations) - 1
        while l<=r:
            mid = (l + r)//2
            if citations[mid]==len(citations)-mid:
                return citations[mid]
            elif citations[mid]<len(citations)-mid:
                l = mid + 1
            else:
                r = mid -1
        return len(citations)-l
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$ 

