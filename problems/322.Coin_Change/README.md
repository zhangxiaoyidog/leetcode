## 322.Coin Change

## 题目描述

给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

**示例 1:**

```
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
```

**示例 2:**

```
输入: coins = [2], amount = 3
输出: -1
```

**说明:**
你可以认为每种硬币的数量是无限的。



### 解答1

​	这道题说白了就是找到符合条件的硬币组合，那么首先想到的当然是使用递归去列举所有的组合，然后找到最少的就行了。但是超时了orz……

```python
import sys
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        return self.coinSearch(0,coins,amount)
    def coinSearch(self,idxCoin,coins,amount):
        if amount==0:
            return 0
        if idxCoin<len(coins) and amount>0:
            max_val = amount//coins[idxCoin]
            minCost = sys.maxsize
            for i in range(max_val+1):
                res = self.coinSearch(idxCoin+1,coins,amount-i*coins[idxCoin])
                if res!=-1:
                    minCost = min(minCost,res+i)
            return -1 if minCost == sys.maxsize else minCost
        return -1
```



### 解答2

​	使用动态规划解题，定义状态dp[i]表示凑成总金额i所需的最少的硬币个数，动态转移的过程如下表：

| name | C1 | C2 | C3 | action | F[i] |
|:-----:|:---:|:---------:|:------:|:-----:|-------|
| 1 | F(0) |  |  | min+1 | 1 |
| 2 | F(1) | F(0) |  | …… | 1 |
| 3 | F(2) | F(1) | F(0) | …… | 1 |
| 4 | F(3) | F(2) | F(1) | …… | 2 |
| 5 | F(4) | F(3) | F(2) | …… | 2 |
| 6 | F(5) | F(4) | F(3) | …… | 2 |



```python
import sys
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [amount+1]*(amount+1) 
        dp[0]=0
        for i in range(1,amount+1):
            for coin in coins:
                if coin<=i:
                    dp[i] = min(dp[i],dp[i-coin]+1)
        return dp[amount] if dp[amount]<=amount else -1
```

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n)$ 

