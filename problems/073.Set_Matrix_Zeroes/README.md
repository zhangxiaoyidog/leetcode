## 073.Set Matrix Zeroes

### 题目描述

给定一个 *m* x *n* 的矩阵，如果一个元素为 0，则将其所在行和列的所有元素都设为 0。请使用**原地**算法**。**

**示例 1:**

```
输入: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
输出: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

**示例 2:**

```
输入: 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出: 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```

### 解答

​	这道题最简单的方式就是使用O(*mn*) 的额外空间，也就是重新开辟一个矩阵大小的空间用来存储原先的数组，遍历这个新数组的过程去改变原数组的值(如果直接遍历矩阵的每一个元素，判断这个元素是不是`0`，如果是的话那么将对应的行和列的元素置为零，但是这种有一个陷阱，因为一旦置为零，那么我们对于没有遍历到的元素就会存在这样的风险：原先不是`0`，但是因为之前有数将其置为`0`了，我们遍历到这个原本是非`0`数的时候就不要将其行和列置为零了)。

​	这里我使用的算法是使用O(*m+n*) 的额外空间，也就是去遍历二维数组，如果`matrix[i][j]==0`，则将`i`存放在`rows`中，将`j`存放在`cols`中，然后再次遍历二维数组，如果发现`i in rows or j in cols`，则把该`cell`的值设为0。

```python
class Solution:
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        m = len(matrix)
        n = len(matrix[0])
        
        row = []
        col = []
        for i in range(m):
            for j in range(n):
                if matrix[i][j]==0:
                    row.append(i)
                    col.append(j)
        for i in range(m):
            for j in range(n):
                if i in row or j in col:
                    matrix[i][j] = 0
```

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n+m)$ 