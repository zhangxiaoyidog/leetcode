## 300.Longest Increasing Subsequence

## 题目描述

给定一个无序的整数数组，找到其中最长上升子序列的长度。

**示例:**

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```

**说明:**

- 可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
- 你算法的时间复杂度应该为 O(*n2*) 。

**进阶:** 你能将算法的时间复杂度降低到 O(*n* log *n*) 吗?



### 解答

​	这道题很明显了，使用动态规划求解，由于上升子序列不一定非要是连续的，所以定义dp[i]表示以nums[i]结尾的最长上升子序列的长度，使用两个for循环遍历即可。

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        # 动态规划,不一定是连续的序列
        if len(nums)==0:
            return 0
        dp = [1]*len(nums)
        res = 1
        
        for i in range(len(nums)):
            max_val = 0
            for j in range(i):
                if nums[i]>nums[j]:
                    max_val = max(max_val,dp[j])
            dp[i] = max_val + 1
            res = max(res,dp[i])
        return res
```

- 时间复杂度：$O(n^2)$
- ​空间复杂度：$O(n)$ 

