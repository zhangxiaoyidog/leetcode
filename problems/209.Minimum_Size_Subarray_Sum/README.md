## 209.Minimum Size Subarray Sum

## 题目描述

给定一个含有 **n** 个正整数的数组和一个正整数 **s ，**找出该数组中满足其和 **≥ s** 的长度最小的连续子数组**。**如果不存在符合条件的连续子数组，返回 0。

**示例:** 

```
输入: s = 7, nums = [2,3,1,2,4,3]
输出: 2
解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。
```

**进阶:**

如果你已经完成了*O*(*n*) 时间复杂度的解法, 请尝试 *O*(*n* log *n*) 时间复杂度的解法。



### 解答

​	再往前遍历的同时sum不断累加，假如超过了限定值，则不断把前界left上的值给删去，这时计算连续子数组的长度，计算出最小的那个值。

```python
import sys

class Solution:
    def minSubArrayLen(self, s: int, nums: 'List[int]') -> int:
        res = sys.maxsize
        if len(nums)==0:
            return 0
        sums = 0
        left = 0
        for i in range(len(nums)):
            sums+=nums[i]
            while sums>=s:
                res = min(res, i-left+1)
                sums -= nums[left]
                left+=1

        if res == sys.maxsize:
            return 0
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 