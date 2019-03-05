## 139.Word Break

## 题目描述

给定一个**非空**字符串 *s* 和一个包含**非空**单词列表的字典 *wordDict*，判定 *s* 是否可以被空格拆分为一个或多个在字典中出现的单词。

**说明：**

- 拆分时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

**示例 1：**

```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
```

**示例 2：**

```
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
```

**示例 3：**

```
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```



### 解答

​	一开始我想用回溯算法来解这道题，有一些特殊例无法AC，想到其实动态规划其实更简单，定义dp[i]表示前i个字母是否可以拆分，那么在计算dp[i]的时候只需要去搜索前i个字母的某一位置j可否拆分以及j->i是否在字典中出现，满足则dp[i]为1，否则为0。

```python
class Solution:
    def wordBreak(self, s: str, wordDict: 'List[str]') -> bool:
        # 使用动态规划
        dp = [0]*(len(s)+1)
        dp[0] = 1
        for i in range(1,len(s)+1):
            for j in range(i):
                # print(s[j:i])
                if dp[j] and s[j:i] in wordDict:
                    dp[i] = 1
                    break
        return dp[len(s)]==1
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 