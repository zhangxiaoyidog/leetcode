## 064.Minimum Path Sum

### 题目描述

给定一个包含非负整数的 *m* x *n* 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。

**示例:**

```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```

### 解答

​	这道题和前面两道题一样，也是使用动态规划解题的经典题目，边界条件还是大同小异，动态转移方程则为上方和左方最小的值加上当前网格的值。

+ 定义状态：grid\[i][j]表示到达这一点的最小路径总和。
+ 初始状态：只能等于自己的上方(列)或者自己左方(行)加上当前网格的值。
+ 状态转移方程：有两种方式，一种是从上方走过来，另一种是从左方走过来，故状态转移方程为:grid\[i][j] += min(grid\[i-1][j],grid\[i][j-1])

```python
class Solution:
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        # 使用动态规划解题,grid[i][j]表示到达这一点的数字总和
        
        #边界
        m = len(grid)
        n = len(grid[0])
        for i in range(1,m):
            grid[i][0] += grid[i-1][0]
        for i in range(1,n):
            grid[0][i] += grid[0][i-1]
        
        
        for i in range(1,m):
            for j in range(1,n):
                grid[i][j] += min(grid[i-1][j],grid[i][j-1])
        return grid[m-1][n-1]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 

