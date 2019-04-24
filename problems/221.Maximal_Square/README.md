## 221.Maximal Square

## 题目描述

在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

**示例:**

```
输入: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4
```



### 解答

​	这种题目一般都是用动态规划求解，但是怎么定义状态是比较重要也是难点所在，一开始我总是想定义为直接结果，也就是最大正方形的面积，这样是非常不直观且分析起来很复杂，所以假如建立一个结果数组，数组中的每个值，保存的是该cell作为最右下角的元素构建正方形所能构建的最大的正方形的边长。

​	有时候做动态规划的题目需要定义这种'中间结果'作为状态，这样就很清晰了，dp\[i][j]表示以第i行第j列为右下角所能构成的最大正方形边长, 则递推式为: dp\[i][j] = 1 + min(dp\[i-1][j-1], dp\[i-1][j], dp\[i][j-1]);

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if len(matrix)==0:
            return 0
        # 使用动态规划解题,dp[i][j]表示第i行第j列为右下角所能构成的最大正方形边长
        dp = [[0]*len(matrix[0]) for i in range(len(matrix))]
        max_l = 0
        # 边界
        for i in range(len(matrix)):
            if matrix[i][0]=='1':
                dp[i][0]=1
                max_l = max(max_l,dp[i][0])
        for i in range(len(matrix[0])):
            if matrix[0][i]=='1':
                dp[0][i]=1      
                max_l = max(max_l,dp[0][i])
                
        for i in range(1,len(matrix)):
            for j in range(1,len(matrix[0])):
                if matrix[i][j]=='1':
                    dp[i][j] = 1 + min(min(dp[i-1][j-1],dp[i-1][j]),dp[i][j-1])
                    max_l = max(max_l,dp[i][j])
        return max_l*max_l
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 