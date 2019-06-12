## 012 Integer to Roman

### 题目描述

罗马数字包含以下七种字符： `I`， `V`， `X`， `L`，`C`，`D` 和 `M`。

```
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

例如， 罗马数字 2 写做 `II` ，即为两个并列的 1。12 写做 `XII` ，即为 `X` + `II` 。 27 写做  `XXVII`, 即为 `XX` + `V` + `II` 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 `IIII`，而是 `IV`。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 `IX`。这个特殊的规则只适用于以下六种情况：

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

给定一个整数，将其转为罗马数字。输入确保在 1 到 3999 的范围内。



**示例 1:**

```
输入: 3
输出: "III"
```

**示例 2:**

```
输入: 4
输出: "IV"
```

**示例 3:**

```
输入: 9
输出: "IX"
```

**示例 4:**

```
输入: 58
输出: "LVIII"
解释: L = 50, V = 5, III = 3.
```

**示例 5:**

```
输入: 1994
输出: "MCMXCIV"
解释: M = 1000, CM = 900, XC = 90, IV = 4.
```



### 解答1：分段讨论

- 建立罗马符号和对应整数的数组；
- 分别讨论当前位（从高位到低位）的大小的不同情况：以x为例。
- 当x<4的情况；当x == 4的情况；当x>4 & x<9的情况；以及当x == 9的情况。

```python
class Solution:
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        roman = ['M','D','C','L','X','V','I']
        value = [1000,500,100,50,10,5,1]
        res = ''
        for i in range(0,7,2):
            x = num // value[i]
            if x < 4:
                for j in range(x):
                    res+=roman[i]
            elif x == 4:
                res += roman[i]
                res += roman[i -1]
            elif 4<x<9:
                res += roman[i-1]
                for j in range(6,x+1):
                    res+=roman[i]
            elif x == 9:
                res += roman[i]
                res += roman[i-2]
            num %= value[i]
        return res
```
复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(m)$ （m为数组大小）



### 解答2：贪婪算法

- 建立罗马符号和对应整数的数组；
- 每次查表找出当前最大的数，减去该数后再继续查表。



```python
class Solution:
    def intToRoman(self, num):
        """
        :type num: int
        :rtype: str
        """
        roman = ["M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"]
        value = [1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1]
        res = ''
        for i in range(len(roman)):
            while num >= value[i]:
                num -= value[i]
                res += roman[i]

        return res
```



复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(m)$ （m为数组大小）