## 028.mplement strStr()

### 题目描述

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与C语言的 [strstr()](https://baike.baidu.com/item/strstr/811469) 以及 Java的 [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)) 定义相符。



### 解答

​	这道题比较简单，我的做法就是使用一个指针向前遍历haystack字符串，判断指针前len(needle)的长度的位置到指针的位置这一段字符串是否和needle相等即可。

```python
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if len(needle)==0:
            return 0
        if len(needle)>len(haystack):
            return -1
        
        for i in range(len(needle), len(haystack)+1):
            if needle == haystack[i - len(needle):i]:
                return i - len(needle)
        return -1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$