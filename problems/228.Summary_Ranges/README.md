## 228.Summary Ranges

## 题目描述

给定一个无重复元素的有序整数数组，返回数组区间范围的汇总。

**示例 1:**

```
输入: [0,1,2,4,5,7]
输出: ["0->2","4->5","7"]
解释: 0,1,2 可组成一个连续的区间; 4,5 可组成一个连续的区间。
```

**示例 2:**

```
输入: [0,2,3,4,6,8,9]
输出: ["0","2->4","6","8->9"]
解释: 2,3,4 可组成一个连续的区间; 8,9 可组成一个连续的区间。
```



### 解答

​	这道题也是常规做法，设置start标志，在遍历的同时取判断条件是否满足即可，最后加上末尾的部分即可得到最终答案。

```python
class Solution:
    def summaryRanges(self, nums: List[int]) -> List[str]:
        res = []
        if len(nums)==0:
            return res
        start = 0
        last = nums[0]
        for i in range(1,len(nums)):
            if nums[i]-last==1:
                last = nums[i]
            else:
                if i-start>0:
                    if i-1==start:
                        res.append(str(nums[start]))
                    else:
                        res.append(str(nums[start])+'->'+str(nums[i-1]))
                    start = i
                    last = nums[i]
        if start==len(nums)-1:
            res.append(str(nums[start]))
        else:
            res.append(str(nums[start])+'->'+str(nums[-1]))
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 