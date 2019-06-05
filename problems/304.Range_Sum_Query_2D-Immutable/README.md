## 304.Range Sum Query 2D - Immutable

## 题目描述

给定一个二维矩阵，计算其子矩形范围内元素的总和，该子矩阵的左上角为 (*row*1, *col*1) ，右下角为 (*row*2, *col*2)。

![Range Sum Query 2D](https://assets.leetcode-cn.com/aliyun-lc-upload/original_images/range_sum_query_2d.png)
上图子矩阵左上角 (row1, col1) = **(2, 1)** ，右下角(row2, col2) = **(4, 3)，**该子矩形内元素的总和为 8。

**示例:**

```
给定 matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```

**说明:**

1. 你可以假设矩阵不可变。
2. 会多次调用 *sumRegion* 方法*。*
3. 你可以假设 *row*1 ≤ *row*2 且 *col*1 ≤ *col*2。



### 解答

​	这道题还是和上面那道题一样的解法，只不过转换到二维矩阵上了，在这里需要判断一些边界条件，也就是这个矩阵是否在边界上的问题。

```python
class NumMatrix:
# [[7, 7, 0],
#  [-4, -7, 7], 
#  [-4, 0, -2], 
#  [-8, -5, 6]]
    def __init__(self, matrix: List[List[int]]):
        if len(matrix)==0:
            return 
        self.matrix = matrix
        self.target = [[0]*len(matrix[0]) for j in range(len(matrix))]
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if i==0 and j==0:
                    self.target[i][j] = matrix[i][j]
                elif i==0:
                    self.target[i][j] = matrix[i][j]+self.target[i][j-1]
                elif j==0:
                    self.target[i][j] = matrix[i][j]+self.target[i-1][j]
                else:
                    self.target[i][j] = matrix[i][j]+self.target[i-1][j]+self.target[i][j-1]-self.target[i-1][j-1]
                    
        print(self.target)
    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        if row1>0 and col1>0:
            return self.target[row2][col2] - self.target[row2][col1-1]-self.target[row1-1][col2]+self.target[row1-1][col1-1]
        elif row1>0:
            return self.target[row2][col2] - self.target[row1-1][col2]
        elif col1>0:
            return self.target[row2][col2] - self.target[row2][col1-1]
        else:
            return self.target[row2][col2]

# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```

