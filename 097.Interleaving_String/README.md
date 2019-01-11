## 097.Interleaving String

## 题目描述

给定三个字符串 *s1*, *s2*, *s3*, 验证 *s3* 是否是由 *s1* 和 *s2* 交错组成的。

**示例 1:**

```
输入: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
输出: true
```

**示例 2:**

```
输入: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
输出: false
```



### 解答

​	这道题如果使用两个指针直接遍历那肯定是出错的，所以看到验证两个字符串和第三个之间的关系的这样的题目很容易想到可以使用动态规划求解，dp\[i][j]表示s1长为i s2长为j的时候能否匹配，这几次在看别人的代码的时候，发现在定义dp数组的时候多申请一个存储长度，这可以便于一一对应，这道题使用这种技巧也会很方便，因为dp\[0][0]就表示两个字符串长度都为0的时候能否匹配，这一个技巧是很方便的。

​	那么这道题边界即为s1为空或者s2为空的时候能否匹配，当前状态与前一个状态和当前值是否相等有关，这里要注意的一点就是，要实时假设s3的长度等于其他两个的长度和，当然这也和我们的dp数组的定义是契合的，动态转移的时候，只需要判断两种情况是否有一种成立即可，具体可以看代码自己理解一下，比较简单。

```python
class Solution:
    def isInterleave(self, s1, s2, s3):
        """
        :type s1: str
        :type s2: str
        :type s3: str
        :rtype: bool
        """
        if len(s3) != len(s1) + len(s2):
            return False

        # 使用动态规划求解 dp[i][j]表示s1长为i s2长为j的时候 能否匹配
        dp = [[0]*(len(s2) + 1) for _ in range(len(s1)+1)]
        # 边界
        dp[0][0] = 1
        # s1 为空
        for i in range(len(s2)):
            if s2[i] == s3[i]:
                dp[0][i + 1] = dp[0][i]
        for i in range(len(s1)):
            if s1[i] == s3[i]:
                dp[i + 1][0] = dp[i][0]     
        
        for i in range(1, len(s1) + 1):
            for j in range(1, len(s2) + 1):
                if (dp[i][j - 1] == 1 and s3[i + j - 1] == s2[j - 1]) or (
                        dp[i - 1][j] == 1 and s3[i + j - 1] == s1[i - 1]):
                    dp[i][j] = 1
        
        return dp[len(s1)][len(s2)]==1
```

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n*m)$ 