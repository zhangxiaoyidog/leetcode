## 383.Ransom Note

### 题目描述

给定一个赎金信 (ransom) 字符串和一个杂志(magazine)字符串，判断第一个字符串ransom能不能由第二个字符串magazines里面的字符构成。如果可以构成，返回 true ；否则返回 false。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。)

**注意：**

你可以假设两个字符串均只含有小写字母。

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```





### 解答

​	采取了最简单粗暴的方法，遍历ransom中的每一个字符，如果在magazine中，就remove掉它，继续判断到最后。

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        if len(ransomNote)==0:
            return True
        m = list(magazine)
        for c in ransomNote:
            if c not in m:
                return False
            m.remove(c)
        return True
```

- 时间复杂度：$O(len(ransom))$
- 空间复杂度：$O(1)$ 