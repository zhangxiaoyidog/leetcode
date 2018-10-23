## 006 ZigZag_Conversion

### 题目描述

将字符串 `"PAYPALISHIRING"` 以Z字形排列成给定的行数：

```
P   A   H   N
A P L S I I G
Y   I   R
```

之后从左往右，逐行读取字符：`"PAHNAPLSIIGYIR"`

实现一个将字符串进行指定行数变换的函数:

```
string convert(string s, int numRows);
```

**示例 1:**

```
输入: s = "PAYPALISHIRING", numRows = 3
输出: "PAHNAPLSIIGYIR"
```

**示例 2:**

```
输入: s = "PAYPALISHIRING", numRows = 4
输出: "PINALSIGYAHRPI"
解释:

P     I    N
A   L S  I G
Y A   H R
P     I
```

​	这道题需要去找这个序列的规律，然后编程解决问题，规律如下所示，我们可以通过一行一行读取的方式来输出整个序列，第一行和最后一行做特殊处理，可以观察到整列之间的差都是2×numRow-2，然后在第i行中间的数字和前面的数字的差都是2×numRow-2-2*i。可以根据这个规律来解题。

```python
0    6      12       0   4   8
1  5 7   11 13       1 3 5 7 9
2 4  8 10   14 *     2   6   10
3    9      15
```

```python
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        
        if len(s)==0 or numRows==0 or numRows==1:
            return s
        # 整列的差
        row_len = 2*numRows - 2 
        s1=''
        for i in range(numRows):
            j = i
            while j<len(s):
                # 先处理整列的数字
                s1+=s[j]
                if i!=0 and i!=numRows-1 and j+row_len-2*i<len(s):
                    s1+=s[j+row_len-2*i]
                j+=row_len
        return s1
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$