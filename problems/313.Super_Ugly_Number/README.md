## 313.Super Ugly Number

## 题目描述

编写一段程序来查找第 n 个超级丑数。

超级丑数是指其所有质因数都是长度为 k 的质数列表 primes 中的正整数。

**示例:**

```输入: n = 12, primes = [2,7,13,19]
输入: n = 12, primes = [2,7,13,19]
输出: 32 
解释: 给定长度为 4 的质数列表 primes = [2,7,13,19]，前 12 个超级丑数序列为：[1,2,4,7,8,13,14,16,19,26,28,32] 。
```

**说明:**

+ 1 是任何给定 primes 的超级丑数。
+  给定 primes 中的数字以升序排列。
+ 0 < k ≤ 100, 0 < n ≤ 106, 0 < primes[i] < 1000 。
+ 第 n 个超级丑数确保在 32 位有符整数范围内。



### 解答

​	这道题的解法和[264](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/264.Ugly_Number_II/README.md)题的解法是差不多的，需要利用之前的计算，这里需要使用len(primes)个指针，分别负责×primes中的数字，每次往数组中添加指针所指的数字乘后的结果中最小的那个，然后把对应的指针加一。

```python
class Solution:
    def nthSuperUglyNumber(self, n: int, primes: List[int]) -> int:
        idx = [0]*len(primes)
        res = [1]
        for i in range(1,n):
            res.append(min([res[idx[j]]*primes[j] for j in range(len(idx))]))
            for j in range(len(idx)):
                if res[-1] == res[idx[j]] * primes[j]:
                    idx[j]+=1
        return res[-1]
```

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(m)$ 