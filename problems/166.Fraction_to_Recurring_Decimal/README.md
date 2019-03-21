## 166.Fraction to Recurring Decimal

## 题目描述

给定两个整数，分别表示分数的分子 numerator 和分母 denominator，以字符串形式返回小数。

如果小数部分为循环小数，则将循环的部分括在括号内。

**示例 1:**

```
输入: numerator = 1, denominator = 2
输出: "0.5"
```

**示例 2:**

```
输入: numerator = 2, denominator = 1
输出: "2"
```

**示例 3:**

```
输入: numerator = 2, denominator = 3
输出: "0.(6)"
```



### 解答

​	这道题还是有点难度的，首先需要判断符号，然后就不用管符号的问题，直接使用绝对值相除。这里有一个技巧就是，有限小数的小数部分是不可能出现相同的数字的，所以可以使用一个字典存储各个小数位的位置，一旦出现重复小数，则在这个位置插入'('，在尾部插入')'。

```python
class Solution:
    def fractionToDecimal(self, numerator: int, denominator: int) -> str:
        ans = ''
        if numerator==0:
            return '0'
        # 判断符号
        if numerator*denominator < 0:
            ans += '-'
        dic = {}
        # 绝对值
        n = abs(numerator)
        d = abs(denominator)
        ans += str(n // d)
        n %= d
        if n == 0:
            return ans
        ans += '.'
        while n:
            #　已出现，则必为循环小数
            if n in dic:
                temp_list = list(ans)
                temp_list.insert(dic[n], '(')
                ans = ''.join(temp_list)
                ans += ')'
                return ans
            # 加入当前的商
            dic[n] = len(ans)
            ans += str(n * 10 // d)
            n = n * 10 % d
        return ans
```

