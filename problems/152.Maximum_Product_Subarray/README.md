## 152.Maximum Product Subarray

## 题目描述

给定一个整数数组 `nums` ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。

**示例 1:**

```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```

**示例 2:**

```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```



### 解答

​	这道题和[53题](https://github.com/zhangxiaoyidog/leetcode/blob/master/053.Maximum_Subarray/README.md)有点相似，但是这一道题是求乘积的最大连续子序列，如果按照之前的思路使用动态规划的一个状态空间来记录以第`i`个元素结尾的连续子数组的最大值，那么肯定是不行的，因为可能会出现连续都是负数，但是乘起来很大的情况，这样之前的思路和做法是没法处理的，所以这里我们的思维不能被固化，这道题是可以用动态固化来求解的，但是需要两个状态空间，一个记录的是以第`i`个元素结尾的连续子数组的最小值，而另一个状态空间记录的是以第`i`个元素结尾的连续子数组的最大值，这么做的原因在于负数*负数为正数的情况。也就是，如果当前元素是负数的话，那么让它乘以之前的最小负数，将会得到一个很大的正数。

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        # 动态规划解题
        if len(nums) == 0:
            return 0
        # 两个状态，一个纪录最大值，一个记录最小值，防止负数×负数的情况出现
        min_dp = [0] * len(nums)
        max_dp = [0] * len(nums)
        min_dp[0] = nums[0]
        max_dp[0] = nums[0]
        res = nums[0]
        for i in range(1,len(nums)):
            min_dp[i] = min(min(min_dp[i-1]*nums[i], max_dp[i-1]*nums[i]), nums[i])
            max_dp[i] = max(max(min_dp[i-1]*nums[i], max_dp[i-1]*nums[i]), nums[i])
            res = max(res,max_dp[i])
            
        return res
                   
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$