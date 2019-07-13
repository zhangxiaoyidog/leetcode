## 387.First Unique Character in a String

### 题目描述

给定一个字符串，找到它的第一个不重复的字符，并返回它的索引。如果不存在，则返回 -1。

**案例:**

```
s = "leetcode"
返回 0.

s = "loveleetcode",
返回 2.
```



**注意事项：**您可以假定该字符串只包含小写字母。



### 解答

​	先采用一个hashmap来遍历存储每个字母是否出现过两次，然后再遍历一次就可以找到第一个不重复的字符了。

```python
class Solution:
    def firstUniqChar(self, s: str) -> int:
        d = {}
        for c in s:
            if c in d:
                d[c] = 0
            else:
                d[c] = 1
        for i,c in enumerate(s):
            if d[c]==1:
                return i
        return -1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 