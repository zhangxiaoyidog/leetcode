## 312.Burst Balloons

## 题目描述

有 n 个气球，编号为0 到 n-1，每个气球上都标有一个数字，这些数字存在数组 nums 中。

现在要求你戳破所有的气球。每当你戳破一个气球 i 时，你可以获得 nums[left] * nums[i] * nums[right] 个硬币。 这里的 left 和 right 代表和 i 相邻的两个气球的序号。注意当你戳破了气球 i 后，气球 left 和气球 right 就变成了相邻的气球。

求所能获得硬币的最大数量。

说明:

```
你可以假设 nums[-1] = nums[n] = 1，但注意它们不是真实存在的所以并不能被戳破。
0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100
```

示例:

```输入: [3,1,5,8]
输入: [3,1,5,8]
输出: 167 
解释: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
     coins =  315      +  358    +  138      + 181   = 167
```



### 解答

​	这道题还是使用动态规划解答，在nums左右都增加一个1哨兵，dp\[i][j]表示表示将 i-j之间的气球戳破获取硬币的最大数量，保留i,j，因为哨兵的气球不能被戳破，则可以遍历i-j之间的位置去戳破来得到最大的数量。假设 k 号气球（i+1<= k <= j-1）是 [i+1...j-1] 中最后一个被戳破的。

```python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        # 使用动态规划，增加两个哨兵
        nums = [1] + nums + [1]
        
        l = len(nums)
        # dp[i][j]表示将 i-j之间的气球戳破获取硬币的最大数量
        dp = [[0]*l for _ in range(l)]
        for j in range(2,l):
            for i in range(j-2,-1,-1):
                for k in range(i+1,j):
                    dp[i][j] = max(dp[i][j],dp[i][k]+nums[i]*nums[k]*nums[j]+dp[k][j])
        return dp[0][-1]
```

- 时间复杂度：$O(n^3)$
- 空间复杂度：$O(n^2)$ 