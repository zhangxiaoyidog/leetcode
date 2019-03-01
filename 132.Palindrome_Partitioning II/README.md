## 132.Palindrome Partitioning II

## 题目描述

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回符合要求的最少分割次数。

**示例:**

```
输入: "aab"
输出: 1
解释: 进行一次分割就可将 s 分割成 ["aa","b"] 这样两个回文子串。
```



### 解答

​	这道题使用动态规划来做，首先要使用isPal\[i][j]表示从i到j位置的子串是否为回文子串，然后用cut[j]表示长度为j时的最小切割次数，可以想到长度为j时，最大的切割次数是j-1，那么我们就可以对位置j遍历之前所有的位置i，如果s[i->j]为回文子串，那么i位置就是一个切割点，在遍历的过程中找到最小的切割次数。

```python
class Solution:
    def minCut(self, s: str) -> int:
        # 使用动态规划
        
        # isPal[i][j]表示i到j是否是回文串
        isPal = [[0]*len(s) for i in range(len(s))]
        cut = [0]*len(s)
    
        for j in range(len(s)):
            min_cut = j
            for i in range(j+1):
                if s[i]==s[j] and (j-i<3 or isPal[i+1][j-1]==1):
                    isPal[i][j]=1
                    if i == 0:
                        min_cut = 0
                    else:
                        min_cut = min(min_cut,cut[i-1] + 1)
            cut[j] = min_cut
        return cut[len(s)-1]
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 

 