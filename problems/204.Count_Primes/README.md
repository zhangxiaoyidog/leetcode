## 204.Count Primes

## 题目描述

统计所有小于非负整数 *n* 的质数的数量。

**示例:**

```
输入: 10
输出: 4
解释: 小于 10 的质数一共有 4 个, 它们是 2, 3, 5, 7 。
```



### 解答1

​	第一种采取暴力解，在遍历每一个数字的同时判断他们是否是质数，判断的方法就是去除以小于它的这些数以及整除小于它的这些数，假如结果一样那么肯定不是质数。但是在处理很大的数字的时候肯定超时。

```python
class Solution:
    def countPrimes(self, n: int) -> int:
        res = 0
        for i in range(2, n):
            flag = 1
            for j in range(2, i):
                if i / j == i // j:
                    flag = 0
                    break
            if flag == 1:
                res += 1
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 



### 解答2

​	上一种解法可以说是从后往前的一种解法，那么我们能不能从前往后呢，我们知道，所有的非质数都可以分解为两个整数的积，那么在遇到一个质数的时候，可以用它去乘以n以内的数字，把得到所有n以内的非质数找出来，那么剩下的都是质数。

```python
class Solution:
    def countPrimes(self, n: int) -> int:
        res = 0
        IsPrime = [0] * n
        for i in range(2,n):
            if IsPrime[i]==0:
                res+=1
                j = i
                while j*i<n:
                    IsPrime[j*i] = 1
                    j+=1
        return res
```

- 时间复杂度：$O(n)​$
- 空间复杂度：$O(n)$ 