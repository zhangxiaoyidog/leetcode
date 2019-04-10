## 205.Isomorphic Strings

## 题目描述

给定两个字符串 **s** 和 **t**，判断它们是否是同构的。

如果 **s** 中的字符可以被替换得到 **t** ，那么这两个字符串是同构的。

所有出现的字符都必须用另一个字符替换，同时保留字符的顺序。两个字符不能映射到同一个字符上，但字符可以映射自己本身。

**示例 1:**

```
输入: s = "egg", t = "add"
输出: true
```

**示例 2:**

```
输入: s = "foo", t = "bar"
输出: false
```

**示例 3:**

```
输入: s = "paper", t = "title"
输出: true
```

**说明:**
你可以假设 **s** 和 **t** 具有相同的长度。



### 解答

​	这道题判断两个字符串是否同构，也就是说建立字符间的一一对应关系，这里用一个字典解决就ok了，总之只要保证两个字符不能映射到同一个字符上，但字符可以映射自己本身，加上判断条件就可以了。

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if len(s)!=len(t):
            return False
        mapping = {}

        for i,j in zip(s,t):
            if i not in mapping:
                if j in mapping.values():
                    return False
                mapping[i] = j
            elif mapping[i]!=j:
                return False
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 