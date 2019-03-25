## 172.Factorial Trailing Zeroes

## 题目描述

给定一个整数 *n*，返回 *n*! 结果尾数中零的数量。

**示例 1:**

```
输入: 3
输出: 0
解释: 3! = 6, 尾数中没有零。
```

**示例 2:**

```
输入: 5
输出: 1
解释: 5! = 120, 尾数中有 1 个零.
```

**说明:** 你算法的时间复杂度应为 *O*(log *n*) 。



### 解答

​	这道题我是打印了很多数字的阶乘找到的规律，计算公式为：令f(x)表示正整数x末尾所含有的“0”的个数，则有：    当0 \< n < 5时，f(n!) = 0;    当n >= 5时，f(n!) = k + f(k!), 其中 k = n / 5（取整）。

​	其实是可以证明的，具体点击[这里](https://www.cnblogs.com/hutonm/p/5624996.html)。

```python
class Solution:
    def trailingZeroes(self, n: int) -> int:
        res = 0
        while n!=0:
            n = n//5
            res+=n
        return res
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$

