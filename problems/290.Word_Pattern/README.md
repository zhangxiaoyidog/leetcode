## 290.Word Pattern

## 题目描述

给定一种规律 `pattern` 和一个字符串 `str` ，判断 `str` 是否遵循相同的规律。

这里的 **遵循** 指完全匹配，例如， `pattern` 里的每个字母和字符串 `str` 中的每个非空单词之间存在着双向连接的对应规律。

**示例1:**

```
输入: pattern = "abba", str = "dog cat cat dog"
输出: true
```

**示例 2:**

```
输入:pattern = "abba", str = "dog cat cat fish"
输出: false
```

**示例 3:**

```
输入: pattern = "aaaa", str = "dog cat cat dog"
输出: false
```

**示例 4:**

```
输入: pattern = "abba", str = "dog dog dog dog"
输出: false
```

**说明:**
你可以假设 `pattern` 只包含小写字母， `str` 包含了由单个空格分隔的小写字母。 



### 解答

​	这道题的解答还是很常规，使用字典的一一对应关系帮助解答，一开始我观察到子母和单词是双相连接的对应规律，所以使用了两个字典，其实一个足够。

```python
class Solution:
    def wordPattern(self, pattern: str, str: str) -> bool:
        words = str.split()
        if len(words)!=len(pattern):
            return False
        dic1 = {}
        dic2 = {}
        for p,word in zip(pattern,words):
            if p not in dic1 and word not in dic2:
                dic1[p] = word
                dic2[word] = p
            elif p in dic1 and word in dic2:
                if dic1[p]!=word or dic2[word]!=p:
                    return False
            else:
                return False
        return True
```

在使用for循环的时候使用index比直接使用zip元素快得多。

```python
class Solution:
    def wordPattern(self, pattern: str, str: str) -> bool:
        words = str.split()
        if len(words)!=len(pattern):
            return False
        dic1 = {}   
        for i in range(len(pattern)):
        # for p,word in zip(pattern,words):
            if pattern[i] not in dic1:
                if words[i] in dic1.values():
                    return False
                dic1[pattern[i]] = words[i]
            else:
                if dic1[pattern[i]]!=words[i]:
                    return False
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

