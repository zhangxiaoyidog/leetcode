## 357.Count Numbers with Unique Digits

### 题目描述

给定一个非负整数 n，计算各位数字都不同的数字 x 的个数，其中 0 ≤ x < 10n 。

**示例:**

```
输入: 2
输出: 91 
解释: 答案应为除去 11,22,33,44,55,66,77,88,99 外，在 [0,100) 区间内的所有数字。
```



### 解答

n=1: res=10

n=2: res=9*9+10=91 # 两位数第一位只能为1-9，第二位只能为非第一位的数，加上一位数的所有结果

n=3: res=9 * 9 * 8+91=739 # 三位数第一位只能为1-9，第二位只能为非第一位的数，第三位只能为非前两位的数，加上两位数的所有结果

n=4: res=9 * 9 * 8 * 7+739=5275 # 同上推法



```python
class Solution:
    def countNumbersWithUniqueDigits(self, n: int) -> int:
        if n==0:
            return 1
        res = 10
        mul = 9
        for i in range(1,n):
            mul*=10-i
            res+=mul
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

