## 378.Kth Smallest Element in a Sorted Matrix

### 题目描述

给定一个 n x n 矩阵，其中每行和每列元素均按升序排序，找到矩阵中第k小的元素。
请注意，它是排序后的第k小元素，而不是第k个元素。

**示例:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,
返回 13。
```

**说明: **
你可以假设 k 的值永远是有效的, 1 ≤ k ≤ n2 。



### 解答

​	这道题由于每一行的第一个数字并不一定比上一行最后一个数字小，所以没法用常规的二分查找的思路，直接求解矩阵中的第8小元素很难，我们可以用二分法设定一个值mid，查看mid值是否是矩阵第8小元素。

​	首先设置mid为矩阵第一个元素和最后一个元素的平均值，然后统计矩阵中每一行小于mid值的个数之和。若该值小于8，记录当前mid，L = mid + 1，并更新mid；若该值大于8，R = mid - 1。 这样的话我们要找的那个数字会始终在L和R之间，最后一定会L和R相遇，并且就等于要找的数字，此时的mid值即为所求。

```python
class Solution:
    def kthSmallest(self, matrix: List[List[int]], k: int) -> int:
        
        def guess(matrix, g, k):
            sum = 0
            for i in range(len(matrix)):
                l = 0
                r = len(matrix)-1
                ans = 0
                while l<=r:
                    mid = l+(r-l)//2
                    # 若某一行值小于g，则应该是最后一个元素的下标 + 1.
                    if matrix[i][mid]<g:
                        ans = mid+1
                        l = mid+1
                    else:
                        r = mid-1
                sum+=ans
            return k>sum
    
        l = matrix[0][0]
        r = matrix[-1][-1]
        res = 0
        while l<=r:
            mid = l+(r-l)//2
            if guess(matrix,mid,k):
                res = mid
                l = mid+1
            else:
                r = mid-1
        return res
```

- 时间复杂度：$O(n*logn)$
- 空间复杂度：$O(1)$ 