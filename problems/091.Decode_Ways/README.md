## 091.Decode Ways

## 题目描述

一条包含字母 `A-Z` 的消息通过以下方式进行了编码：

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

给定一个只包含数字的**非空**字符串，请计算解码方法的总数。

**示例 1:**

```
输入: "12"
输出: 2
解释: 它可以解码为 "AB"（1 2）或者 "L"（12）。
```

**示例 2:**

```
输入: "226"
输出: 3
解释: 它可以解码为 "BZ" (2 26), "VF" (22 6), 或者 "BBF" (2 2 6) 。
```



### 解答

​	这答题稍微仔细想一下就能想到可以使用动态规划来解题，并且转移方程的定义也比简单，dp[i]就表示长度为i+1的时候的解码方法的总数。这道题提交后战胜了100%的提交记录:D

+ 初始状态dp[0] = 1
+ 转移方程，这里需要分情况讨论：
  + 假如s[i]为‘0’，判断和前一个字母是否能被解码，即判断前一个字母是否为‘0’或者大于2，这样直接返回0，否则如果i为1，则dp[2]直接为1，不然dp[i] = dp[i-2]
  + s[i]不为‘0’,，也有两种情况，首先第一种是判断和前一个字母是否能被解码，即`10 <= int(s[i-1]+s[i]) <= 26`，这时候如果i为1，则dp[2]为2，不然dp[i] = dp[i-1] + dp[i-2] 。第二种情况就是大于26，这种直接dp[i] = dp[i-1]

```python
class Solution:
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        # 使用动态规划解题
        if len(s) == 0 or s[0] == '0':
            return 0
        dp = [0] * len(s)
        # 边界
        dp[0] = 1
        for i in range(1, len(s)):
            if s[i] == '0':
                if (s[i-1] == '0' or int(s[i-1]) > 2):
                    return 0
                else:
                    if i == 1:
                        dp[i] = dp[i-1]
                    else:
                        dp[i] = dp[i-2]
        
            elif 10 <=int(s[i-1]+s[i]) <= 26:
                if i == 1:
                    dp[i] = dp[i-1]+1
                else:
                    dp[i] = dp[i-1]+dp[i-2]
            else:
                dp[i] = dp[i-1]
        return dp[len(s)-1]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 