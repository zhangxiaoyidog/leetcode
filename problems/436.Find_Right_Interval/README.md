## 436.Find Right Interval

## 题目描述

给定一组区间，对于每一个区间 i，检查是否存在一个区间 j，它的起始点大于或等于区间 i 的终点，这可以称为 j 在 i 的“右侧”。

对于任何区间，你需要存储的满足条件的区间 j 的最小索引，这意味着区间 j 有最小的起始点可以使其成为“右侧”区间。如果区间 j 不存在，则将区间 i 存储为 -1。最后，你需要输出一个值为存储的区间值的数组。

**注意:**

1. 你可以假设区间的终点总是大于它的起始点。
2. 你可以假定这些区间都不具有相同的起始点。

**示例 1:**

```
输入: [ [1,2] ]
输出: [-1]

解释:集合中只有一个区间，所以输出-1。
```

**示例 2:**

```
输入: [ [3,4], [2,3], [1,2] ]
输出: [-1, 0, 1]

解释:对于[3,4]，没有满足条件的“右侧”区间。
对于[2,3]，区间[3,4]具有最小的“右”起点;
对于[1,2]，区间[2,3]具有最小的“右”起点。
```

**示例 3:**

```
输入: [ [1,4], [2,3], [3,4] ]
输出: [-1, 2, -1]

解释:对于区间[1,4]和[3,4]，没有满足条件的“右侧”区间。
对于[2,3]，区间[3,4]有最小的“右”起点。
```



### 解答

​	一开始想直接暴力遍历，但是过不了，想到其实可以用二分找最小的右区间，前提是把输入的区间先排序存起来。

```python
class Solution:
    def findRightInterval(self, intervals: List[List[int]]) -> List[int]:
        left_ix = [[intervals[i][0],i] for i in range(len(intervals))]
        # print(left_ix)
        left_ix.sort()
        # print(left_ix)
        res = []
        n = len(intervals)
        for interval in intervals:
            this_end = interval[1]
            l, r = 0, n-1
            while l<r:
                mid = l + (r-l)//2
                if left_ix[mid][0]<this_end:
                    l = mid + 1
                else:
                    r = mid
            if l==n-1 and left_ix[l][0]<this_end:
                res.append(-1)
            else:
                res.append(left_ix[l][1])
        return res
```

- 时间复杂度：$O(n*logn)$
- 空间复杂度：$O(1)$