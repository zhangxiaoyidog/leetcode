## 371.Sum of Two Intergers

### 题目描述

不使用运算符 + 和 - ，计算两整数 a 、b 之和。

**示例 1:**

```
输入: a = 1, b = 2
输出: 3
```


**示例 2:**

```
输入: a = -2, b = 3
输出: 1
```



### 解答

​	这道题可以使用投机取巧的方法`sum([a,b])`，但是常规做法还是使用二进制运算，假如不考虑进位，a+b可以表示为a^b(比如0010 ^ 0110 = 0110)，进位的那一位则表示为a＆b(比如0010 & 0110 = 0010)进位则使用<<运算，所以最终的值是把这二者相加。不过这里要小心负数，也就是-1+1的这种情况，因为python中会把负数转换成long，如-1^1=-2，-1&1=2，在 Python 中，整数不是 32 位的，也就是说你一直循环左移并不会存在溢出的现象，这就需要我们手动对 Python 中的整数进行处理，手动模拟 32 位 INT 整型。

```python
import math
class Solution:
    def getSum(self, a: int, b: int) -> int:
        # return math.log(math.exp(a)*math.exp(b))
        # 2^32
        MASK = 0x100000000
        # 整型最大值
        MAX_INT = 0x7FFFFFFF
        MIN_INT = MAX_INT + 1
        while b!=0:
            # 计算进位
            c = (a & b)<<1
            # 无进位
            a = (a ^ b)%MASK
             
            b = c%MASK
            
        return a if a <= MAX_INT else ~((a % MIN_INT) ^ MAX_INT)
```

