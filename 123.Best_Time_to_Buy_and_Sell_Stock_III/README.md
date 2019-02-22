## 123.Best Time to Buy and Sell Stock III

## 题目描述

给定一个数组，它的第 *i* 个元素是一支给定的股票在第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 *两笔* 交易。

**注意:** 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入: [3,3,5,0,0,3,1,4]
输出: 6
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```

**示例 2:**

```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3:**

```
输入: [7,6,4,3,1] 
输出: 0 
解释: 在这个情况下, 没有交易完成, 所以最大利润为 0。
```

### 解答１

​	第一种就是使用动态规划来解题，使用状态dp\[i][j]来表示进行了i次交易的第j天的最大收益，因此我们可以遍历所有的时间，求得最大的那个收益，然后状态转移和上一道题差不多，取上一天和当前天的最大者，实际上这道题可以转化成可进行k次交易，用这个模板也是可行的。但是很遗憾，提交超时。

```python
class Solution:
    def maxProfit(self, prices: 'List[int]') -> 'int':
        # 动态规划解题 dp[i][j]表示进行了i次交易，并且已知第j天的价格时的最大收益
        if len(prices)<2:
            return 0
        dp = [[0]*len(prices) for i in range(3)]
        # print(dp)
        # 控制交易次数
        for i in range(1,3):
            # 两个for循环遍历所有结果
            for j in range(1,len(prices)):
                profit = 0
                for k in range(j):
                    profit = max(profit,dp[i-1][k]+prices[j]-prices[k])
                
                dp[i][j] = max(dp[i][j-1],profit)
 

        return dp[2][len(prices)-1]
```

- 时间复杂度：$O(k*n^2)$
- 空间复杂度：$O(k*n)$ 



### 解答2

​	在评论区看到一种方法十分巧妙，并且时间复杂度非常低，具体思路为对于任意一天考虑四个变量，分别对四个变量进行相应的更新, 最后secSell就是最大，收益值(secSell >= fstSell)。

+ fstBuy: 在该天第一次买入股票可获得的最大收益

+ fstSell: 在该天第一次卖出股票可获得的最大收益

+ secBuy: 在该天第二次买入股票可获得的最大收益

+ secSell: 在该天第二次卖出股票可获得的最大收益

  

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        # 一次遍历
        buy1 = buy2 = float("-inf")
        sell1 = sell2 = 0
        for p in prices:
            buy1 = max(buy1,-p)
            sell1 = max(sell1,buy1+p)
            buy2 = max(buy2,sell1-p)
            sell2 = max(sell2,buy2+p)
        return max(sell1,sell2)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 