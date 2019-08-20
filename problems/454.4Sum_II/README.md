## 454.4Sum II

## 题目描述

给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -228 到 228 - 1 之间，最终结果不会超过 231 - 1 。

例如:

```
输入:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

输出:
2

解释:
两个元组如下:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0

```

### 解答

​	这道题先用一个dict把前两个数所有加和的可能情况记录下来，转换成两数之和的情况即可。

```python
class Solution(object):
    def fourSumCount(self, A, B, C, D):
        """
        :type A: List[int]
        :type B: List[int]
        :type C: List[int]
        :type D: List[int]
        :rtype: int
        """
        ab_map = {}
        count = 0
        for a in A:
            for b in B:
                ab_map[a+b] = ab_map.get(a+b,0)+1
        for c in C:
            for d in D:
                temp = -(c+d)
                if temp in ab_map:
                    count+=ab_map[temp]
        return count
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$