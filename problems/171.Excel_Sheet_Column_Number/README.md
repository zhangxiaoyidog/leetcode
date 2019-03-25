## 171.Excel Sheet Column Number

## 题目描述

给定一个Excel表格中的列名称，返回其相应的列序号。

例如，

```
    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...
```

**示例 1:**

```
输入: "A"
输出: 1
```

**示例 2:**

```
输入: "AB"
输出: 28
```

**示例 3:**

```
输入: "ZY"
输出: 701
```



### 解答

​	这道题和之前的那道[Excel表列名称](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/168.Excel_Sheet_Column_Title/README.md)是相反的操作，其实这道题就类似于进制相互转换而已，没什么难的。

```python
class Solution:
    def titleToNumber(self, s: str) -> int:
        i = len(s) - 1 
        res = 0
        # 其实就是进制转换
        for l in s:
            res += (ord(l)-64) * (26**i)
            i-=1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$