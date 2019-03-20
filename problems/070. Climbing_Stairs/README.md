## 070.Climbing Stairs

### 题目描述

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

**示例 1：**

```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```

**示例 2：**

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```



### 解答

​	这道题目我在005这个题目里面的动态规划专栏中已经提到过，有很多种解法，但是动态规划是最合理的解答，这道题也是动态规划的经典题目，详细请点[这里](https://github.com/zhangxiaoyidog/leetcode/blob/master/005.Longest_Palindromic_Substring/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92.md)，所以这里就不再过多赘述。

```python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        # 动态规划经典题目
        if n <=3 :
            return n
        dp = [0 for i in range(n)]
        dp[0] = 1
        dp[1] = 2
        for i in range(2,n):
            dp[i] = dp[i-1] + dp[i-2]
        return dp[n-1]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 