## 396.Rotate Function

### 题目描述

给定一个长度为 n 的整数数组 A 。

假设 Bk 是数组 A 顺时针旋转 k 个位置后的数组，我们定义 A 的“旋转函数” F 为：

F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1]。

计算F(0), F(1), ..., F(n-1)中的最大值。

**注意:**
可以认为 n 的值小于 105。

示例:

```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

所以 F(0), F(1), F(2), F(3) 中的最大值是 F(3) = 26 。
```





### 解答1

​	一开始就是写了一个函数来旋转数组，然后一个个计算，但是提交超时。

```python
class Solution:
    def maxRotateFunction(self, A: List[int]) -> int:
        def rotate(A,k):
            return A[len(A)-k:]+A[:len(A)-k]
        if len(A)==0:
            return 0
        temp = float("-inf")
        for i in range(len(A)):
            B = rotate(A,i)
            sums = 0
            for j in range(len(B)):
                sums+=j*B[j]
            if sums>=temp:
                temp = sums
        return temp
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 



### 解答2

​	两个相邻的F是有规律的，找出规律求解。



```python
class Solution:
    def maxRotateFunction(self, A: List[int]) -> int:
        if len(A)==0:
            return 0
        sums = 0
        for i in range(len(A)):
            sums+=i*A[i]
        temp = sums
        sumA = sum(A)
        # F(j) = F(j-1)+sum(A)-len(A)*A[-j]
        for j in range(1,len(A)):
            sums = sums+sumA-len(A)*A[-j]
            temp = max(temp,sums)
        return temp
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 