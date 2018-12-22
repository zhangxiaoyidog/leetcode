## 067.Add Binary

### 题目描述

给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为**非空**字符串且只包含数字 `1` 和 `0`。

**示例 1:**

```
输入: a = "11", b = "1"
输出: "100"
```

**示例 2:**

```
输入: a = "1010", b = "1011"
输出: "10101"
```



### 解答

​	这道题很简单，使用之前两个链表相加的思想，也就是同时去遍历相加，然后判断输出，最后遍历长度更长的字符串的刚刚未遍历的那部分即可。

```python
class Solution(object):
    def addBinary(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        m = len(a) - 1
        n = len(b) - 1
        res = ''
        flag = 0
        while m >= 0 or n >= 0:
            temp = flag
            if m>=0:
                temp+=int(a[m])
            if n>=0:
                temp+=int(b[n])
            res = str(temp%2)+res
            flag = temp//2
            m -= 1
            n -= 1
        if flag == 1:
            res = '1' + res
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)​$ 