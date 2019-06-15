## 326.Power of Three

## 题目描述

给定一个整数，写一个函数来判断它是否是 3 的幂次方。

**示例 1:**

```
输入: 27
输出: true
```

**示例 2:**

```
输入: 0
输出: false
```

**示例 3:**

```
输入: 9
输出: true
```

**示例 4:**

```
输入: 45
输出: false
```

**进阶：**
你能不使用循环或者递归来完成本题吗？



### 解答1

```python
class Solution:
    def isPowerOfThree(self, n: int) -> bool:
        index = 1
        while index<n:
            index*=3
        return index==n
```



### 解答2

​	使用对数来解决，很巧妙。

```python
import math
class Solution:
    def isPowerOfThree(self, n: int) -> bool:
        if n<=0:
            return False
        r = math.log10(n)/math.log10(3)
        return r==int(r)
```

