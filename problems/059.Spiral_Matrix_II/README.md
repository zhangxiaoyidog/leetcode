## 059.**Spiral Matrix II**

### 题目描述

给定一个正整数 *n*，生成一个包含 1 到 *n*2 所有元素，且元素按顺时针顺序螺旋排列的正方形矩阵。

**示例:**

```
输入: 3
输出:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

### 解答

​	这道题和之前的那个题思路大概一直，也就是一层一层去遍历赋值，这里我遇到了一个问题就是数组的初始化问题：如果用`matrix = [[0 for i in range(n)] for i in range(n)]`，则是正确的初始化，假如用`[[0]*n]*n`这样的做法则会出错，因为这样list 里面的元素都是同一个对象，会同时改变值，这一点要注意。具体思路看代码即可。

```python
class Solution:
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if n==0:
            return[[]]
        matrix = [[0 for i in range(n)] for i in range(n)]
        # 一层一层去填充
        
        row_begin = 0
        row_end = n-1
        col_begin = 0
        col_end = n-1
        value = 1
        # 由于是正方形矩阵，只需要判断一个维度就行
        while row_begin<=row_end:
            for i in range(col_begin,col_end + 1):
                matrix[row_begin][i] = value
                value+=1
            # 大于1行才执行 
            if row_end>row_begin:
                for j in range(row_begin+1,row_end+1):
                    matrix[j][col_end]=value
                    value+=1
             # 大于两行两列才执行
            if row_end>row_begin and col_end>col_begin:
                for i in range(col_end-1,col_begin-1,-1):
                    matrix[row_end][i]=value
                    value+=1
              # 大于三行两列才执行
            if row_end - 1 > row_begin and col_end > col_begin:
                for j in range(row_end - 1, row_begin, -1):
                    matrix[j][col_begin]=value
                    value+=1
            row_begin += 1
            row_end -= 1
            col_begin += 1
            col_end -= 1
        return matrix
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n^2)$ 