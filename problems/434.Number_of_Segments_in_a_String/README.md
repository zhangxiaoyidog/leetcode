## 434.Number of Segments in a String

## 题目描述

统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

**示例:**

```
输入: "Hello, my name is John"
输出: 5
```



### 解答

​	其实用python的内置函数split只需要一行吧，但是这样也太没品了，所以还是遍历，在最后加一个' '，然后遍历判断遇到的空格，但是前面一个字母不能是空格。

```python
class Solution:
    def countSegments(self, s: str) -> int:
        count = 0
        s+=' '
        for i in range(len(s)):
            if s[i] == ' ' and s[i-1]!=' ':
                count+=1 
        return count
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$