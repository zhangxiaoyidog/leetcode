## 029.**Divide Two Integers**

### 题目描述

给定两个整数，被除数 `dividend` 和除数 `divisor`。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 `dividend` 除以除数 `divisor` 得到的商。

**示例 1:**

```
输入: dividend = 10, divisor = 3
输出: 3
```

**示例 2:**

```
输入: dividend = 7, divisor = -3
输出: -2
```

**说明:**

- 被除数和除数均为 32 位有符号整数。
- 除数不为 0。
- 假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。

### 解答1

​	这道题不准使用乘法、除法和mod运算符，所以一开始我想到的就是使用减法，然后比较减后的结果和除数决定是否继续减，但是这样会时间超时,而且一开始代码写得很冗余。

```Python
class Solution:
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        maxint = 0x7fffffff;
        minint = 0x80000000;
        if divisor == 0:
            return maxint
        if dividend == 0:
            return 0
        flag = 1
        if dividend < 0:
            flag = -1
            dividend = -dividend
        if divisor < 0:
            flag = -1 * flag
            divisor = -divisor
        i = 0
        while dividend >= divisor:
            dividend -= divisor
            i += 1

        if i * flag < -minint or i * flag > maxint:
            return maxint
        return flag * i
```

- 时间复杂度：$O(n)$(这里的n指的是最后结果大小)
- 空间复杂度：$O(1)$



### 解答2	

​	不让使用乘除法，那就可以使用对数运算和指数运算来代替，然后优化一下代码，完美解决问题。

```python
import math
class Solution:
    def divide(self, dividend, divisor):
        """
        :type dividend: int
        :type divisor: int
        :rtype: int
        """
        maxint = 0x7fffffff;
        minint = 0x80000000;
        if divisor == 0:
            return maxint
        if dividend == 0:
            return 0
        flag = (divisor<0) == (dividend<0)
        dividend = abs(dividend)
        divisor = abs(divisor)
        res = math.log(dividend) - math.log(divisor)
        res = int(math.exp(res))
        if flag:
            return min(res,maxint)
        return max(0-res,-minint)
```

- 时间复杂度：$O(1)$
- 空间复杂度：$O(1)$