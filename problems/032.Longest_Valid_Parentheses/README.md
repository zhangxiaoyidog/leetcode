## 032.Longest Valid Parentheses

### 题目描述

给定一个只包含 `'('` 和 `')'` 的字符串，找出最长的包含有效括号的子串的长度。

**示例 1:**

```
输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
```

**示例 2:**

```
输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"
```

### 解答1

​	第一种思路无非就是暴力法，穷举所有的可能的结果，然后使用之前的括号判断方法去判断是否规范即可，但是时间复杂度直接爆炸。

```python
class Solution:
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        max_l = 0
        x = 0
        for i in range(len(s)):
            for j in range(i+2,len(s)+1):
                if self.isvalid(s[i:j]):
                    x = max(j-i,max_l)
                    max_l = x
        return x
    
    def isvalid(self,s):
        stack = []
        flag= 1
        for c in s:
            if c == '(':
                stack.append(c)
            else:
                if len(stack) != 0:
                    stack.pop()
                else:
                    flag = 0
        if flag==0 or len(stack)!=0:
            return False
        return True
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$

### 解答2

​	第二种方法就是使用动态规划来解决问题，把握好动态规划的三要素(边界、最优子结构，状态转移方程)，所以可以按照如下的方式去使用动态规划求解：

+ 状态定义
  + 定义dp[i]表示以s[i]结尾的子串的最大有效括号对
+ 初始状态
  + dp[0]=0
+ 转移方程
  + 如果当前遇到的字符为‘(’，则此时不可能是有效的括号对，所以dp[i]=0
  + 如果上一个字符为‘)’，那么此时可能可能会出现()()这种子串，所以需要定位到到以`s[i-1]`结尾的最长有效括号对的上一个位置，如果是`(`，则`dp[i]=dp[i-1]+dp[i-dp[i-1]-2]+2`。

```python
class Solution:
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        dp = [0 for i in range(len(s))]
        max_l = 0
        if len(s) == 0:
            return 0

        for i in range(1, len(s)):
            if s[i] == ')':
                if s[i - 1] == '(':
                    dp[i] = (dp[i - 2] if i >= 2 else 0) + 2
                elif s[i - dp[i - 1] - 1] == '(' and i - dp[i - 1] > 0:
                    dp[i] = dp[i - 1] + (dp[i - dp[i - 1] - 2] if i - dp[i - 1] >= 2 else 0) + 2
            # else:
            #     dp[i] = dp[i - 1]
            max_l = max(max_l, dp[i])

        return max_l
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$