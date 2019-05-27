## 279.Perfect Squares

## 题目描述

给定正整数 *n*，找到若干个完全平方数（比如 `1, 4, 9, 16, ...`）使得它们的和等于 *n*。你需要让组成和的完全平方数的个数最少。

**示例 1:**

```
输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.
```

**示例 2:**

```
输入: n = 13
输出: 2
解释: 13 = 4 + 9.
```



### 解答

​	这道题是使用动态规划解题，首先定义dp数组，dp[n] 表示以n为和的最少平方的和的个数，dp 数组所有下标已经为完全平方数的数（如1,4,9...）置为 1，加一层 j 遍历找到当前 i 下长度最小的组合。动态方程的意思是：对于每个 i ，比 i 小一个完全平方数的那些数中最小的个数+1就是所求，也就是 dp [ i - j * j ] + 1 。但是我写的这个版本是超时的。

```python
import sys
class Solution:
    def numSquares(self, n: int) -> int:
        
        dp = [sys.maxsize]*(n+1)
        i = 1
        while i*i<=n:
            dp[i*i] = 1
            i+=1
        # j = 1
        for i in range(1,n+1):
            j = 1
            while j*j<i:
                dp[i] = min(dp[i],dp[i-j*j]+1)
                j+=1
        return dp[n]
```



再看看官方的版本，提交ac，但是感觉差不多啊?仔细看看少了很多对比的运算。

```python

class Solution:
    def numSquares(self, n: int) -> int:
        dp = [0]
        for i in range(1,n+1):
            dp.append(min(dp[-j*j] for j in range(1, 1 + int(i**0.5))) + 1)
        return dp[-1]
```



