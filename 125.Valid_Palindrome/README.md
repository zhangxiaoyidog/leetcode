## 125.Valid Palindrome

## 题目描述

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：**本题中，我们将空字符串定义为有效的回文串。

**示例 1:**

```
输入: "A man, a plan, a canal: Panama"
输出: true
```

**示例 2:**

```
输入: "race a car"
输出: false
```



### 解答

​	这道题比较容易想到的就是使用头尾两个指针同时往中间遍历判断，判断的时候过滤掉一些不符合的字符即可。

​	也有其他的解决方案，比如使用python中的filter方法，把字符串处理一下，然后和它的反转比较一下也是可以的。

```python
class Solution:
    def isPalindrome(self, s: 'str') -> 'bool':
        if len(s)<2:
            return True
        s = s.lower()
        start = 0
        end = len(s)-1
        while start<end:
            # 两个游标同时往中间遍历判断
            if (not s[start].isalpha()) and (not s[start].isdigit()):
                start+=1
                continue
            if (not s[end].isalpha()) and (not s[end].isdigit()):
                end-=1
                continue
            if s[start]!=s[end]:
                return False
            start += 1
            end -= 1
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 