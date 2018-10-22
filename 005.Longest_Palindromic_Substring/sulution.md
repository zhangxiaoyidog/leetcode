## 005 **Longest_Palindromic_Substring**

### 题目描述

给定一个字符串 **s**，找到 **s** 中最长的回文子串。你可以假设 **s** 的最大长度为1000。

**示例:**

```
示例 1：

输入: "babad"
输出: "bab"
注意: "aba"也是一个有效答案。

示例 2：

输入: "cbbd"
输出: "bb"
```

## 解答1

​	使用暴力法求解，这道题可以穷举所有可能的子字符串，然后判断这个子字符串是不是回文子串就行，但是这样的揭发时间复杂度会非常高，提交后系统显示超时/(ㄒoㄒ)/~~。

```python
import operator
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        max_len = 0
        if len(s) ==0:
            return ''
        re_s = s[0]
        for i in range(len(s)):
            for j in range(i+1,len(s)+1):
                this_s = s[i:j]
                this_c_rev = ''.join(list(reversed(this_s)))
                if operator.eq(this_s,this_c_rev) and len(this_s)>=max_len:
                    max_len = len(this_s)
                    re_s = this_s
        return re_s
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

## 解答2

​	中心扩展法，利用回文子串的特点，它肯定是一个中心对称的字符串，也就是可以遍历字符串中的每一个元素，每次以这个字符为中心可以判断一个字符和它周围的元素是否对称，然后往周围延伸。这里需要注意的是要分两种情况，一种是有中心元素，比如ababd，一种没有比如acc。虽然最大的时间复杂度为$O(n^2)$，但是一般实际运行没有第一种时间长。

```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        max_len = 0
        if len(s) == 0:
            return ''
        if len(s) == 1 or (len(s) == 2 and s[0] == s[1]):
            return s
        flag = 0
        for i in range(len(s) - 1):
            if i - 1 >= 0 and s[i - 1] == s[i + 1]:
                flag = 1
                j = i - 1
                k = i + 1
                while j > 0 and k < len(s)-1 and s[j - 1] == s[k + 1]:
                    j -= 1
                    k += 1
                if max_len < k - j + 1:
                    max_len = k - j + 1
                    low = j
            if s[i] == s[i + 1]:
                flag = 1
                j = i
                k = i+1
                while j > 0 and k < len(s)-1 and s[j - 1] == s[k + 1]:
                    j -= 1
                    k += 1
                if max_len < k - j + 1:
                    max_len = k - j + 1
                    low = j
        if flag == 0:
            return s[-1]

        return s[low:max_len + low]
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

## 解答3

​	利用动态规划的思想，回文字符串的子串也是回文，比如P[i,j]（表示从i开始j结束的子串）是回文子串，那么P[i+1,j-1]也是回文子串，这样就可以分解成一系列子问题了。

> * P[i, j] = P[i+1, j-1]， if ( s[i]==s[j] )。 
> * P[i, j] = 0，if ( s[i] != s[j] )

```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        length = len(s)
        matrix_t = [[0 for i in range(length)] for i in range(length)]
        max_len = 0
        longest_str = ''
        for j in range(0,length):
            for i in range(0,j+1):
                if j - i <=1:
                    if s[i]==s[j]:
                        matrix_t[i][j]=1
                        if max_len < j-i+1:
                            max_len = j-i+1
                            longest_str = s[i:j+1]
                else:
                    if s[i]==s[j] and matrix_t[i+1][j-1]:
                        matrix_t[i][j]=1
                        if max_len < j-i+1:
                            max_len = j-i+1
                            longest_str = s[i:j+1]
        return longest_str

```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$

