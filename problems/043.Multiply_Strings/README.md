## 043.Multiply Strings

### 题目描述

给定两个以字符串形式表示的非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的乘积，它们的乘积也表示为字符串形式。

**示例 1:**

```
输入: num1 = "2", num2 = "3"
输出: "6"
```

**示例 2:**

```
输入: num1 = "123", num2 = "456"
输出: "56088"
```

**说明：**

1. `num1` 和 `num2` 的长度小于110。
2. `num1` 和 `num2` 只包含数字 `0-9`。
3. `num1` 和 `num2` 均不以零开头，除非是数字 0 本身。
4. **不能使用任何标准库的大数类型（比如 BigInteger）**或**直接将输入转换为整数来处理**。

### 解答１

​	因为不能直接转成数字进行计算，那就只能一位一位地计算，类似与我们平时在草稿上计算乘法一样的计算过程，使用两个for循环来控制就行。

```python
class Solution:
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        # """
        answer = 0
        for i, n1 in enumerate(reversed(num1)):
            for j, n2 in enumerate(reversed(num2)):
                answer += int(n1) * (10 ** i) * int(n2) * (10 ** j)
        return str(answer)
```

复杂度分析：

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(1)$ 

### 解答2

​	第二种做法是网上的做法，就是程序中不出现指数运算，那就要使用一个数组来存储中间结果。时间复杂度差不多，但是没有指数运算会快一些。

```python
class Solution:
    def multiply(self, num1, num2):
        """
        :type num1: str
        :type num2: str
        :rtype: str
        # """
        answer = [0] * (len(num1) + len(num2))
        for i, n1 in enumerate(reversed(num1)):
            for j, n2 in enumerate(reversed(num2)):
                answer[i + j] += int(n1) * int(n2)
                answer[i + j + 1] += answer[i + j] // 10
                answer[i + j] %= 10
        while len(answer) > 1 and answer[-1] == 0:
            answer.pop()
        return ''.join(map(str, answer[::-1]))
```

复杂度分析：

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n)$ 