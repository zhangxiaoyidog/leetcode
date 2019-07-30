## 435.Non-overlapping Intervals

## 题目描述

给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

**注意:**

1. 可以认为区间的终点总是大于它的起点。
2. 区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

**示例 1:**

```
输入: [ [1,2], [2,3], [3,4], [1,3] ]

输出: 1

解释: 移除 [1,3] 后，剩下的区间没有重叠。
```


**示例 2:**

```
输入: [ [1,2], [1,2], [1,2] ]

输出: 2

解释: 你需要移除两个 [1,2] 来使剩下的区间没有重叠。
```


**示例 3:**

```
输入: [ [1,2], [2,3] ]

输出: 0

解释: 你不需要移除任何区间，因为它们已经是无重叠的了。
```



### 解答

​	这道题其实就是区间调度问题，只不过最后返回的是移除的数量，其实没有差别，先按照结束时间排序，然后一直贪心选取最早结束时间即可。

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:
        # 区间调度问题 贪心算法
        res = 0
        intervals.sort(key=lambda x:x[1])
        # print(intervals)
        last = float('-inf')
        
        for i in range(len(intervals)):
            if last <= intervals[i][0]:
                res += 1
                last = intervals[i][1]
        return len(intervals)-res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$