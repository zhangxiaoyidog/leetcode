## 057.Insert Interval

给出一个无重叠的 ，按照区间起始端点排序的区间列表。

在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。

**示例 1:**

```
输入: intervals = [[1,3],[6,9]], newInterval = [2,5]
输出: [[1,5],[6,9]]
```

**示例 2:**

```
输入: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出: [[1,2],[3,10],[12,16]]
解释: 这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
```

### 解答

​	这道题的话可以直接把这个区间加入到我们的区间列表中，然后按照[56题](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/056.Merge_Intervals/README.md)的思路合并即可。

```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        intervals.append(newInterval)
        intervals = sorted(intervals)
        
        res = []
        start_cur = intervals[0][0]
        end_cur = intervals[0][1]
        
        for i in range(1,len(intervals)):
            if intervals[i][0]<=end_cur:
                end_cur = max(end_cur,intervals[i][1])
            else:
                res.append([start_cur,end_cur])
                start_cur = intervals[i][0]
                end_cur = intervals[i][1]
        
        res.append([start_cur,end_cur])
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 