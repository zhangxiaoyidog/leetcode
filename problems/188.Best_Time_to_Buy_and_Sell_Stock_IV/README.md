## 188.Best Time to Buy and Sell Stock IV

## 题目描述

给定一个数组，它的第 *i* 个元素是一支给定的股票在第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 **k** 笔交易。

**注意:** 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入: [2,4,1], k = 2
输出: 2
解释: 在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。
```

**示例 2:**

```
输入: [3,2,6,5,0,3], k = 2
输出: 7
解释: 在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```



### 解答

​	这道题我是继续延续了[123](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/123.Best_Time_to_Buy_and_Sell_Stock_III/README.md)的一个做法，使用动态规划来求解。但是很遗憾超时orz……

```python
class Solution:
    def maxProfit(self, k: int, prices: List[int]) -> int:
        # 使用动态规划 dp[i][j]表示进行了i次交易，并且已知第j天的价格时的最大收益
        if len(prices)<2 or k < 1:
            return 0
        
        dp = [[0]*len(prices) for i in range(k+1)]
        
        for i in range(1, k+1):
            max_profit = 0
            for j in range(len(prices)):
                
                for l in range(j):
                    max_profit = max(max_profit,dp[i-1][l] + prices[j] - prices[l])
                dp[i][j] = max(max_profit,dp[i][j-1])
        print(dp)
        return dp[k][len(prices) - 1]

```

- 时间复杂度：$O(k*n^2)$
- 空间复杂度：$O(k*n)$ 

