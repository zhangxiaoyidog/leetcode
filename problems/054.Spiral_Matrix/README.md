## 054.**Spiral Matrix**

### 题目描述

给定一个包含 *m* x *n* 个元素的矩阵（*m* 行, *n* 列），请按照顺时针螺旋顺序，返回矩阵中的所有元素。

**示例 1:**

```
输入:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
输出: [1,2,3,6,9,8,7,4,5]
```

**示例 2:**

```
输入:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
输出: [1,2,3,4,8,12,11,10,9,5,6,7]
```

### 解答

​	这道题并没有很难，只要用四个循环去输出各个边的数就行，详细的细节看代码即可。

```python
class Solution:
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        if not matrix:
            return []
        row_begin = 0
        row_end = len(matrix) - 1
        col_begin = 0
        col_end = len(matrix[0]) - 1
        res = []
        # 一层一层遍历

        while row_begin <= row_end and col_begin <= col_end:
            for i in range(col_begin, col_end + 1):
                res.append(matrix[row_begin][i])

            # 大于1行才执行
            if row_end > row_begin:
                for j in range(row_begin + 1, row_end + 1):
                    res.append(matrix[j][col_end])
            # 大于两行两列才执行
            if row_end > row_begin and col_end > col_begin:
                for i in range(col_end - 1, col_begin - 1, -1):
                    res.append(matrix[row_end][i])
            # 大于三行两列才执行
            if row_end - 1 > row_begin and col_end > col_begin:
                for j in range(row_end - 1, row_begin, -1):
                    res.append(matrix[j][col_begin])
            row_begin += 1
            row_end -= 1
            col_begin += 1
            col_end -= 1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 