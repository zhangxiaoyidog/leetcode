## 168.Excel Sheet Column Title

## 题目描述

给定一个正整数，返回它在 Excel 表中相对应的列名称。

例如，

```
    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB 
    ...
```

**示例 1:**

```
输入: 1
输出: "A"
```

**示例 2:**

```
输入: 28
输出: "AB"
```

**示例 3:**

```
输入: 701
输出: "ZY"
```



### 解答

​	这道题直接不停取余然后去整除就能得到结果了。

```python
class Solution:
    def convertToTitle(self, n: int) -> str:
        # ord(s) ascii码 chr(a) ascii码为a的字母
        res = ''
        while n > 0:
            n-=1
            res = chr(ord('A') + n%26) + res
            n//=26
        return res
```

