## 121.Best Time to Buy and Sell Stock

## 题目描述

给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```

**示例 2:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```



### 解答１

​	第一种就是使用暴力解法，两个for循环遍历，得到最大的收益。但是很遗憾，提交超时。

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
        profit = prices[1] - prices[0]
        for i in range(len(prices)):
            for j in range(i+1,len(prices)):
                if prices[j]-prices[i]>=profit:
                    profit = prices[j]-prices[i]
        if profit<=0:
            return 0
        return profit
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 



### 解答2

​	需要想办法降低时间复杂度，假如给定[7, 1, 5, 3, 6, 4]，我们在图表上绘制给定数组中的数字，我们将会得到：

![Profit Graph](https://leetcode-cn.com/media/original_images/121/121_profit_graph.png)

​	使我们感兴趣的点是上图中的峰和谷。我们需要找到最小的谷之后的最大的峰。 我们可以维持两个变量——minprice 和 maxprofit，它们分别对应迄今为止所得到的最小的谷值和最大的利润（卖出价格与最低价格之间的最大差值）。

​	其实也可以使用动态规划这种空间换时间的方式，也很简单，前i天的最大收益 = max{前i-1天的最大收益，第i天的价格-前i-1天中的最小价格}。

```python
class Solution:
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        # 一次遍历
        
        if len(prices)<2:
            return 0
        min_price = prices[0]
        profit = 0
        for i in range(1,len(prices)):
            if prices[i]<=min_price:
                min_price = prices[i]
                #print(min_price)
            elif profit<=prices[i]-min_price:
                profit = prices[i]-min_price

        return profit
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 