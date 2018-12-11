## 048.**Rotate Image**

### 题目描述

给定一个 *n* × *n* 的二维矩阵表示一个图像。

将图像顺时针旋转 90 度。

**说明：**

你必须在**原地**旋转图像，这意味着你需要直接修改输入的二维矩阵。**请不要**使用另一个矩阵来旋转图像。

**示例 1:**

```
给定 matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

原地旋转输入矩阵，使其变为:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**示例 2:**

```
给定 matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

原地旋转输入矩阵，使其变为:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

### 解答

这道题其实需要去找一下旋转的规律，也就是可以采用两步走来解决问题，首先以对角线为轴旋转一下，然后交换列，例子如下所示。



****

1  2  3　　　 　　 **9  6**  3　　　　　  **7  4  1**

4  5  6　　-->　　 **8**  5  **2**　　 -->   　 8  5  2　　

7  8  9 　　　 　　7  **4  1**　　　　　  **9  6  3**





```python
class Solution:
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        h = len(matrix)
        # 先以对角线为轴旋转
        for i in range(h - 1):
            for j in range(h - i - 1):
                temp = matrix[i][j]
                matrix[i][j] = matrix[h - 1 - j][h - 1 - i]
                matrix[h - 1 - j][h - 1 - i] = temp
        # 然后交换列
        for i in range(h // 2):
            for j in range(h):
                temp = matrix[i][j]
                matrix[i][j] = matrix[h - 1 - i][j]
                matrix[h - 1 - i][j] = temp
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 

