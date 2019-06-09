## 309.Best Time to Buy and Sell Stock with Cooldown

## 题目描述

给定一个整数数组，其中第 i 个元素代表了第 i 天的股票价格 。

设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

+ 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
+ 卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。

示例:

```
输入: [1,2,3,0,2]
输出: 3 
解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]
```



### 解答

​	这道题和之前的股票问题有些类似，但是这里的不同之处在于这道题加了一个冷冻期，这里维护三个状态，sell[i]表示截至第i天，最后一个操作是卖时的最大收益；buy[i]表示截至第i天，最后一个操作是买时的最大收益；cool[i]表示截至第i天，最后一个操作是冷冻期时的最大收益；最后返回sell[-1]即可。

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices)==0:
            return 0
        # sell[i]表示截至第i天，最后一个操作是卖时的最大收益；
        # buy[i]表示截至第i天，最后一个操作是买时的最大收益；
        # cool[i]表示截至第i天，最后一个操作是冷冻期时的最大收益；
        sell = [0]*len(prices)
        buy = [0]*len(prices)
        cool = [0]*len(prices)
        buy[0] = -prices[0]
        for i in range(1,len(prices)):
            sell[i] = max(buy[i-1]+prices[i],sell[i-1])
            # buy之前必须有一个cool
            buy[i] = max(cool[i-1]-prices[i],buy[i-1])
            # 保证这一天啥也不干就行
            cool[i] = max(buy[i-1],sell[i-1],cool[i-1])
        return sell[-1]
```

- 时间复杂度：$O(n)$
- ​空间复杂度：$O(n)$ 