## 115.Distinct Subsequences

## 题目描述

给定一个字符串 **S **和一个字符串 **T**，计算在 **S** 的子序列中 **T** 出现的个数。

一个字符串的一个子序列是指，通过删除一些（也可以不删除）字符且不干扰剩余字符相对位置所组成的新字符串。（例如，`"ACE"` 是 `"ABCDE"` 的一个子序列，而 `"AEC"` 不是）

**示例 1:**

```
输入: S = "rabbbit", T = "rabbit"
输出: 3
解释:

如下图所示, 有 3 种可以从 S 中得到 "rabbit" 的方案。
(上箭头符号 ^ 表示选取的字母)

rabbbit
^^^^ ^^
rabbbit
^^ ^^^^
rabbbit
^^^ ^^^

```

**示例 2:**

```
输入: S = "babgbag", T = "bag"
输出: 5
解释:

如下图所示, 有 5 种可以从 S 中得到 "bag" 的方案。 
(上箭头符号 ^ 表示选取的字母)

babgbag
^^ ^
babgbag
^^    ^
babgbag
^    ^^
babgbag
  ^  ^^
babgbag
    ^^^
```

### 解答

​	还是之前说过的，看到两个字符串和子字符串这样的题目就需要想到我们的动态规划算法，这一题也是比较简单。

```python
class Solution:
    def numDistinct(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: int
        """
        # 这个题要想到用动态规划做
        # dp[i][j]表示s长度为i，t长度为j时的方案
        dp = [[0]*(len(t)+1) for i in range(len(s)+1)]
        #print(dp)
        # 边界,当t长度为0时,只有一种方案
        
        for i in range(len(s)+1):
            dp[i][0] = 1
        #print(dp)
        for i in range(1,len(s)+1):
            for j in range(1,len(t)+1):
                if s[i-1] == t[j-1]:
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j]
        return dp[len(s)][len(t)]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 

