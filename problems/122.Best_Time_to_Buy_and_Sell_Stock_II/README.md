## 122.Best Time to Buy and Sell Stock II

## 题目描述

给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
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
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

### 解答１

​	第一种就是使用暴力解法，两个for循环遍历，里面加一个递归操作，得到最大的收益。但是很遗憾，提交超时。

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        # 暴力解
        if len(prices)<2:
            return 0
        #profit = prices[1] - prices[0]
        res = 0
        # 遍历每种可能性
        for i in range(len(prices)):
            max_temp = 0
            for j in range(i+1,len(prices)):
                if prices[j]>prices[i]:
                    profit = prices[j]-prices[i]
                    if j<len(prices)-1:
                        profit+=self.maxProfit(prices[j+1:])
                    if profit>max_temp:
                        max_temp = profit
            if res<max_temp:
                res = max_temp
        return res
```

- 时间复杂度：$O(n^n)$ (调用递归函数$n^n$次)
- 空间复杂度：$O(n)$  (递归深度)



### 解答2

​	使用动态规划解题，用dp[i]表示第i+1天的最大收益，这一天可以卖出也可以不卖出，这里有一个误区就是其实一天可以卖出再买入，没有影响。所以如果在这一天卖出，需要找到前i-1天中价格最低的那天进行买入，这就需要循环遍历找到，如果不卖出，则与前一天的收益相同。

​	但是动态规划也提示超时，无法AC……

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        # 一次遍历
        
        # 动态规划
        if len(prices)<2:
            return 0
        dp = [0] * len(prices)
        
        for i in range(1,len(prices)):
            max_temp = 0
            for j in range(0,i):
                if dp[j]+prices[i]-prices[j]>max_temp:
                    max_temp = dp[j]+prices[i]-prices[j]
            dp[i] = max(dp[i-1],max_temp)
        return dp[len(prices)-1]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 



### 解答3

​	上面两种方法都不行，只能降低时间复杂度到n，最好的解决方法就是贪心算法了，只关注局部最优解，以得到整体最优，只要股票赚钱了就卖，我们先看一个例子，对于[1,2,3,5]这样的情况，显然5-1可以获得最大的收入，但是由于不限制交易次数，我们也可以这样交易(2-1) + (3-2) + (5-3)，想想看，其实对于[1,2,3,5,3,6]这样的情况也是成立的，提交AC。

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        # 贪心
        if len(prices)<2:
            return 0
        profit = 0
        for i in range(1,len(prices)):
            if prices[i]>prices[i-1]:
                profit += prices[i]-prices[i-1]
        return profit
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 