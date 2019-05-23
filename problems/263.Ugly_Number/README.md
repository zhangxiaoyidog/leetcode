## 263.Ugly Number II

## 题目描述

编写一个程序判断给定的数是否为丑数。

丑数就是只包含质因数 `2, 3, 5` 的**正整数**。

**示例 1:**

```
输入: 6
输出: true
解释: 6 = 2 × 3
```

**示例 2:**

```
输入: 8
输出: true
解释: 8 = 2 × 2 × 2
```

**示例 3:**

```
输入: 14
输出: false 
解释: 14 不是丑数，因为它包含了另外一个质因数 7。
```

**说明：**

1. `1` 是丑数。
2. 输入不会超过 32 位有符号整数的范围: [−231,  231 − 1]。



### 解答

​	这道题如果使用遍历的方式肯定是超时的，那么就使用循环除或者递归的方式得到结果。

```python
class Solution:
    def isUgly(self, num: int) -> bool:
        if num<=0:
            return False
        if num==1:
            return True
        while num>1:
            if num%2==0:
                num //= 2
            elif num%3==0:
                num //= 3
            elif num%5==0:
                num //= 5
            else:
                return False
        return True
```

