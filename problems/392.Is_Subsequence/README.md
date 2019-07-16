## 392.Is Subsequence

### 题目描述

给定字符串 s 和 t ，判断 s 是否为 t 的子序列。

你可以认为 s 和 t 中仅包含英文小写字母。字符串 t 可能会很长（长度 ~= 500,000），而 s 是个短字符串（长度 <=100）。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，"ace"是"abcde"的一个子序列，而"aec"不是）。

**示例 1:**
s = "abc", t = "ahbgdc"

返回 true.

**示例 2:**
s = "axc", t = "ahbgdc"

返回 false.

后续挑战 :

如果有大量输入的 S，称作S1, S2, ... , Sk 其中 k >= 10亿，你需要依次检查它们是否为 T 的子序列。在这种情况下，你会怎样改变代码？



### 解答

​	使用两个指针一个个比对就行了，一开始还以为会超时，原来大家都用的这种解法。

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        k = 0
        if len(s)==0:
            return True
        if len(t)==0:
            return False
        for c in t:
            if c==s[k]:
                k+=1
            if k==len(s):
                return True
            # print(k)
        return False
```



