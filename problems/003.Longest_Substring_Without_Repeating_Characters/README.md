## 003. Longest Substring Without Repeating Characters

### 题目描述

给定一个字符串，找出不含有重复字符的**最长子串**的长度。

**示例:**

```python
示例 1:

输入: "abcabcbb"
输出: 3 
解释: 无重复字符的最长子串是 "abc"，其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 无重复字符的最长子串是 "b"，其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 无重复字符的最长子串是 "wke"，其长度为 3。
     请注意，答案必须是一个子串，"pwke" 是一个子序列 而不是子串。
```

### 解答1

​	这道题一开始我选择的是暴力求解法，思路大概是用两个for循环嵌套，第一个循环控制游标一个一个字母向前移动，第二个for循环来寻找以这个字母开头的无重复最长子串的长度，最终返回更新后的值。

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        max_len = 1
        if len(s) == 0:
            return 0
        for i in range(len(s)-1):
            count = 1
            for index in range(i+1,len(s)):
                if s[index] not in s[i:index]:
                    count+=1
                    if max_len<=count:
                        max_len = count
                else:
                    break
        return max_len
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$



### 解答2

​	利用滑动窗口，创建一个字典来存储字母的位置，代表窗口的大小，循环中往里面添加字母，遇到重复字母则更新start的值为下一个字母的index，计算游标位置到start的距离为最大距离，字典中最大可能存储所有的字母，则空间复杂度为$O(n)$。

```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        # 滑动窗口
        """
        :type s: str
        :rtype: int
        """
        d = {}
        start = 0
        length = 0
        for i,c in enumerate(s):
            if c in d:
                start = max(start,d[c]+1)
            d[c] = i
            length = max(length,i-start+1)
        return length
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

