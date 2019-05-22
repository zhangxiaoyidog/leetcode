## 258.Add Digits

## 题目描述

给定一个非负整数 `num`，反复将各个位上的数字相加，直到结果为一位数。

**示例:**

```
输入: 38
输出: 2 
解释: 各位相加的过程为：3 + 8 = 11, 1 + 1 = 2。 由于 2 是一位数，所以返回 2。
```

**进阶:**
你可以不使用循环或者递归，且在 O(1) 时间复杂度内解决这个问题吗？



### 解答

​	这道题我就是采用循环的方式，外面一个循环控制num是否为一位数，里面的循环控制num各个位置的数字是否相加完毕。

```python
class Solution:
    def addDigits(self, num: int) -> int:
        res = 0
        while num%10!=num:
            while num>0:
                res += num%10
                num//=10
            num = res
            res = 0
        return num
```

