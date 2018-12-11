## 050.Pow(x, n)

### 题目描述

实现 pow(*x*, *n*) ，即计算 x 的 n 次幂函数。

**示例 1:**

```
输入: 2.00000, 10
输出: 1024.00000
```

**示例 2:**

```
输入: 2.10000, 3
输出: 9.26100
```

**示例 3:**

```
输入: 2.00000, -2
输出: 0.25000
解释: 2-2 = 1/22 = 1/4 = 0.25
```

**说明:**

- -100.0 < *x* < 100.0
- *n* 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。

### 解答1

​	首先想到的当然是暴力求解啦，遍历n然后不停做乘法就好了，但是这样时间复杂度很高，超时orz。

```python
class Solution:
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        res = x
        if n == 0:
            return 1
        flag = 0
        if n < 0:
            n = -n
            flag = 1
        # n = -n if n < 0 else n
        
        for i in range(n-1):
            res *=x
        res = 1/res if flag == 1 else res
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	那就要想一想如何降低时间复杂度呢？其实可以使用递归来降低，举个例子，4个3相乘可以转化为2个3相乘后再做一个平方，5个的话就在乘一次3，这样时间复杂度至少降一半。

```python
class Solution:
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        if n <0:
            return 1/self.power(x,-n)
        return self.power(x,n)
    def power(self,x,n):
        # n>0
        if n == 0:
            return 1
        res = self.power(x,n//2)
        if n%2==1:
            res = res*res*x
        else:
            res = res*res
        return res
```

- 时间复杂度：$O(log_2n)$
- 空间复杂度：$O(1)$ 

