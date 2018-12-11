## 053.Maximum Subarray

### 题目描述

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

**示例:**

```
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**进阶:**

如果你已经实现复杂度为 O(*n*) 的解法，尝试使用更为精妙的分治法求解。

### 解答1

首先是暴力枚举所有可能的情况，时间复杂度较高，超时了。

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        res = nums[0]
        
        for i in range(len(nums)):
            sums = 0
            for j in range(i,len(nums)):
                sums +=nums[j]
                if sums>=res:
                    res = sums
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 

### 解答2

​	暴力枚举虽然简单，但是这样的做法是很愚蠢的，其实降低时间复杂度的点很巧妙，这里要换一种思维，也就是假如只遍历一遍数组，在遍历的过程中若当前sum小于0，那么直接抛弃就行，因为我直接拿当前的num开始(sum为0，也就是前缀为0)不比继续往上加更大吗？，所以遵循这个原则即可解题，而这个思想也就是我们常说的贪心算法了。

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        res = nums[0]
        sums = 0
        for num in nums:
            if sums>0:
                sums += num
            else:
                sums = num
            res = max(res,sums)
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答3

​	第三种解法就是使用动态规划来解题，首先定义转移方程，dp[i]即表示以nums[i]结尾的连续子数组的最大和，它可能是`dp[i-1]+nums[i]`或`nums[i]`，初始状态即为nums[0]。

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 动态规划解题
        res = nums[0]
        dp = [nums[0]]
        for i in range(1,len(nums)):
            dp.append(max(dp[i-1]+nums[i],nums[i]))
            res = max(res,dp[i])
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 