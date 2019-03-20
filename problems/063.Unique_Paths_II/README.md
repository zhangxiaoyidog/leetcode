## 063.Unique Paths II

### 题目描述

一个机器人位于一个 *m x n* 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

**说明：***m* 和 *n* 的值均不超过 100。

**示例 1:**

```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
解释:
3x3 网格的正中间有一个障碍物。
从左上角到右下角一共有 2 条不同的路径：
1. 向右 -> 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右 -> 向右
```



### 解答

​	这道题和上一道题很相似，还是使用动态规划解题，只不过需要添加一些特殊点的判断，比如在边界赋值的时候，需要判断前一个点是否可达，在动态转移方程这块需要判断这个点是否可达，不可达的点 还是设置为0，这样加起来等于没加，把握好特殊点即可通过。

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        # dp[i][j]表示到达这个格子的不同的路径，它和dp[i-1][j]和dp[i][j-1]
        # 边界
        m = len(obstacleGrid)
        n = len(obstacleGrid[0])
        if obstacleGrid[0][0] == 1:
            return 0
        obstacleGrid[0][0] = 1
        for i in range(1, m):
            obstacleGrid[i][0] = 1 if obstacleGrid[i][0] == 0 and obstacleGrid[i - 1][0] == 1 else 0
        for i in range(1, n):
            obstacleGrid[0][i] = 1 if obstacleGrid[0][i] == 0 and obstacleGrid[0][i - 1] == 1 else 0
        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j] != 1:
                    obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1]
                else:
                    obstacleGrid[i][j] = 0

        return obstacleGrid[m - 1][n - 1]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 

