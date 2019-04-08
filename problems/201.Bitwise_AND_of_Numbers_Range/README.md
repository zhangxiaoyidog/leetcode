## 201.Bitwise AND of Numbers Range

## 题目描述

给定范围 [m, n]，其中 0 <= m <= n <= 2147483647，返回此范围内所有数字的按位与（包含 m, n 两端点）。

**示例 1:** 

```
输入: [5,7]
输出: 4
```

**示例 2:**

```
输入: [0,1]
输出: 0
```



### 解答1

​	这道题如果直接使用位运算连起来所有的数，那肯定是超时的，所以得想一个其他的办法，想一下，求所有数字的按位与，假如在某一个数的某一位置有一个0，那么最终结果这一位肯定是0，所以可以直接从最大数往最小与运算，直到与完的结果小于或等于下边界。n&(n-1)会把最后一个1后面所有位都置为0，中间的数字就可以不用管了。

```python
class Solution:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        # res = m
        # # 超时
        # for i in range(m,n+1):
        #     res = res&i
        # return res
        
        while n > m:
            n &= (n-1)
        return n
```



### 解答2

​	第二种我们换一下思路，其实也差不多，这道题其实可以看做是求这些数字的最大公共前缀。

```python
class Solution:
    def rangeBitwiseAnd(self, m: int, n: int) -> int:
        res = 0
        while m!=n:
            n>>=1
            m>>=1
            res+=1
        return m<<res
```

