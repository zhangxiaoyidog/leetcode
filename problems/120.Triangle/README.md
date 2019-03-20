## 120.Triangle

## 题目描述

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

例如，给定三角形：

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

自顶向下的最小路径和为 `11`（即，**2** + **3** + **5** + **1** = 11）。

**说明：**

如果你可以只使用 *O*(*n*) 的额外空间（*n* 为三角形的总行数）来解决这个问题，那么你的算法会很加分。



### 解答1

​	这道题跟前面杨辉三角的题目很相似，第一种解法就是使用动态规划，dp数组存储到当前点的最短路径和，转移方程为:min(dp\[i-1][j] + triangle\[i][j],dp\[i-1][j-1] + triangle\[i][j])，也是比较简单的题目。

```python
class Solution:
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        #解法1 使用动态规划解题 二维数组
        dp = []
        if len(triangle)==0:
            return 0
        dp = [[triangle[0][0]]]
        for i in range(1,len(triangle)):
            temp = []
            for j in range(i+1):
                # 边界两个点
                if j==0:
                    temp.append(dp[i-1][j] + triangle[i][j])
                elif j==i:
                    temp.append(dp[i-1][j-1] + triangle[i][j])
                # 中间点
                else:
                    temp.append(min(dp[i-1][j] + triangle[i][j],dp[i-1][j-1] + triangle[i][j]))
            dp.append(temp)
        return min(dp[len(triangle)-1])
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 



### 解答２

​	看了评论区，有一种解法比较巧妙，这里也记录下来，非常简单直观，也就是倒三角遍历加和，具体细节看代码即可。

```python
class Solution:
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        #　解法2 倒三角遍历加和
        for i in range(len(triangle)-2, -1, -1):
            for j in range(len(triangle[i])):
                triangle[i][j] += min(triangle[i+1][j],triangle[i+1][j+1])
        return triangle[0][0]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)​$ 