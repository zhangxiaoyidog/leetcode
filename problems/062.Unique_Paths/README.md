## 062.Unique Paths

### 题目描述

一个机器人位于一个 *m x n* 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

例如，上图是一个7 x 3 的网格。有多少可能的路径？

**说明：***m* 和 *n* 的值均不超过 100。

**示例 1:**

```
输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右
```

**示例 2:**

```
输入: m = 7, n = 3
输出: 28
```



### 解答

​	这道题一看就得想到使用动态规划解题了，某一个网格肯定是和它的左边网格和上面网格的值有关的(如果存在)，也就是只能从它的左边和上面走过来，并且不需要判断很多情况，直接相加即可，边界`dp[0][0] =1` `dp[i][0] = 1` `dp[0][j] = 1`，动态转移方程dp\[i][j] = dp\[i-1][j] + dp\[i][j-1]。

```python
class Solution:
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        # 我想到可以用动态规划做 
        # dp[i][j]表示到达这个格子的不同的路径，它和dp[i-1][j]和dp[i][j-1]
        dp = [[0 for i in range(n)] for j in range(m)]
        
        # 边界
        for i in range(m):
            dp[i][0] = 1
        for i in range(n):
            dp[0][i] = 1
        
        for i in range(1,m):
            for j in range(1,n):
                dp[i][j] = dp[i-1][j]+dp[i][j-1]
        
        return dp[m-1][n-1]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 