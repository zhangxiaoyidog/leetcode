## 240.Search a 2D Matrix II

## 题目描述

编写一个高效的算法来搜索 *m* x *n* 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

- 每行的元素从左到右升序排列。
- 每列的元素从上到下升序排列。

**示例:**

现有矩阵 matrix 如下：

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。



### 解答

​	由于每行的元素和每列的元素都是有序的，那么可以先判断target在哪一行，也就是用每一行最后一个元素和target去比较，然后就在这一行去找找就可以了。

​	注意这里有序，其实可以用二分查找。

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
        i = 0
        j = len(matrix[0])-1
        while i<len(matrix) and j>=0:
            if matrix[i][j]==target:
                return True
            elif matrix[i][j]<target:
                i+=1
            else:
                j-=1
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 