## 118.Pascal's Triangle

## 题目描述

给定一个非负整数 *numRows，*生成杨辉三角的前 *numRows* 行。

![img](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

在杨辉三角中，每个数是它左上方和右上方的数的和。

**示例:**

```
输入: 5
输出:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```



### 解答

​	这答题之前学习数学的数列的时候就有接触过，也就是后面的序列和前面有关，这种采用动态规划的数组去解题很合适，就是一些细节需要注意一下。

```python
class Solution:
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        # 使用动态规划解题
        
        if numRows == 0:
            return []
        res = [[1]]
        for i in range(1,numRows):
            temp = []
            for j in range(i+1):
                if j == 0 or j == i:
                    temp.append(1)
                else:
                    temp.append(res[i-1][j]+res[i-1][j-1])
            res.append(temp)
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 