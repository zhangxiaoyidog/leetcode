## 056.Merge Intervals

### 题目描述

给出一个区间的集合，请合并所有重叠的区间。

**示例 1:**

```
输入: [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
```

**示例 2:**

```
输入: [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。
```

### 解答

​	其实这个题的难点在于怎么去不停合并的这个过程，难道是合并一个再从头遍历吗？当然不是，这里我觉得一个比较巧妙的地方在于用了两个哨兵去记录start和end，从而达到一次合并多个区间的目的，当然首先我们要对整个数组根据区间的上界进行一个排列，然后再去合并，合并的时候只需要遍历比较当前区间的start和哨兵end的关系即可进行记录和合并，详细直接看代码，也比较容易的。

```python
# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        if len(intervals)<2:
            return intervals
        intervals = sorted(intervals,key=lambda startone:startone.start)
        
        res = []
        start_cur = intervals[0].start
        end_cur = intervals[0].end
        
        for i in range(1,len(intervals)):
            if intervals[i].start<=end_cur:
                end_cur = max(end_cur,intervals[i].end)
            else:
                res.append(Interval(start_cur,end_cur))
                start_cur = intervals[i].start
                end_cur = intervals[i].end
        
        res.append(Interval(start_cur,end_cur))
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 