## 409.Longest Palindrome

### 题目描述

给定一个包含大写字母和小写字母的字符串，找到通过这些字母构造成的最长的回文串。

在构造过程中，请注意区分大小写。比如 "Aa" 不能当做一个回文字符串。

**注意:**
假设字符串的长度不会超过 1010。

**示例 1:**

```
输入:
"abccccdd"

输出:
7

解释:
我们可以构造的最长的回文串是"dccaccd", 它的长度是 7。
```



### 解答

​	这道题不需要解出能构造的最长的回文串，只是需要找出最大长度，观察回文串的特点，需要对称的两个字母是相同的，也就是说至少需要一个字母个数为2，或为其他的偶数，那么直接统计字母个数，把所有偶数个**或者**个数大于等于3(3个我只要2个)的字母个数找出来就行了，最后要注意如果所有的都为偶数那就直接返回s的长度。

```python
class Solution:
    def longestPalindrome(self, s: str) -> int:
        dic = {}
        for c in s:
            dic[c] = dic.get(c,0)+1
        # print(dic)
        res = 0
        for key,value in dic.items():
            if value%2==0:
                res+=value
            elif value!=1:
                res+=value-1
        if res==len(s):
            return res
        return res+1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 