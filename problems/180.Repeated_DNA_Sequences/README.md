## 180.Repeated DNA Sequences

## 题目描述

所有 DNA 由一系列缩写为 A，C，G 和 T 的核苷酸组成，例如：“ACGAATTCCG”。在研究 DNA 时，识别 DNA 中的重复序列有时会对研究非常有帮助。

编写一个函数来查找 DNA 分子中所有出现超多一次的10个字母长的序列（子串）。

**示例:**

```
输入: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

输出: ["AAAAACCCCC", "CCCCCAAAAA"]
```

### 解答

​	这道题我是把所有的可能的序列都找出来了，然后和他们出现的次数一起存在字典中，假如出现了两次，那么加入到res中返回。

```python
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        if len(s)<11:
            return []
        d = {}
        res = []
        for i in range(len(s)-9):
            key = s[i:i+10]
            d[key] = d.get(key,0)+1
            if d.get(key,0)==2:
                res.append(key)
        return res                
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)​$