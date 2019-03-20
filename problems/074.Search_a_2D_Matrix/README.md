## 074.Search a 2D Matrix

### 题目描述

编写一个高效的算法来判断 *m* x *n* 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

- 每行中的整数从左到右按升序排列。
- 每行的第一个整数大于前一行的最后一个整数。

**示例 1:**

```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
输出: true
```

**示例 2:**

```
输入:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
输出: false
```

### 解答1

​	最容易想到的解法是直接遍历，这样复杂度是很高的，所以我想可以先行遍历时直接判断target是否在一头一尾两个元素之间，也就是先确定在哪一行，然后去遍历这一行，这样时间复杂度会降低。

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if len(matrix)==0 or len(matrix[0])==0:
            return False
        m = len(matrix)
        n = len(matrix[0])
        flag = 0
        # 确定行
        for i in range(m):
            if matrix[i][0]<=target<=matrix[i][n-1]:
                flag = 1
                break
          
        if flag == 1:
            # 遍历这一行
            for j in range(n):
                if matrix[i][j] == target:
                    return True
        return False
```

- 时间复杂度：$O(n+m)$
- 空间复杂度：$O(1)$ 



### 解答2

​	这个问题归根结底也是一个查找问题，说起查找问题，我们最有力的工具当然必须是二分查找，所以可以当成一个有序数组的二分查找问题来做，事实证明确实快了不少！！！

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if len(matrix)==0 or len(matrix[0])==0:
            return False
        m = len(matrix)
        n = len(matrix[0])
        low = 0
        high = m*n - 1
        while low<=high:
            mid = (low+high)//2
            if matrix[mid//n][mid%n] == target:
                return True
            elif matrix[mid//n][mid%n] < target:
                low = mid+1
            else:
                high = mid-1
        return False
```

- 时间复杂度：$O(log(mn))$
- 空间复杂度：$O(1)$ 

