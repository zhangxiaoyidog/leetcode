## 415.Add Strings

### 题目描述

给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

**注意：**

1. num1 和num2 的长度都小于 5100.
2. num1 和num2 都只包含数字 0-9.
3. num1 和num2 都不包含任何前导零。
4. **你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。**



### 解答

​	使用两个指针从两个str的最低位往前加就完事了。但是要注意进位。

```python
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:
        # 双指针
        i = len(num1)-1
        j = len(num2)-1
        res = 0
        k = 0
        flag = 0
        res = ''
        while i>=0 or j>=0 or flag:
            if i>=0:
                temp1 = int(num1[i])
            else:
                temp1 = 0
            if j>=0:
                temp2 = int(num2[j])
            else:
                temp2 = 0
                
            temp = temp1+temp2+flag
            flag = temp//10
            res = str(temp%10) + res
            if i>=0:
                i-=1
            if j>=0:
                j-=1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

