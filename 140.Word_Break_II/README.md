## 140.Word Break II

## 题目描述

给定一个**非空**字符串 *s* 和一个包含**非空**单词列表的字典 *wordDict*，在字符串中增加空格来构建一个句子，使得句子中所有的单词都在词典中。返回所有这些可能的句子。

**说明：**

- 分隔时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

**示例 1：**

```
输入:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
输出:
[
  "cats and dog",
  "cat sand dog"
]
```

**示例 2：**

```
输入:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
输出:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
解释: 注意你可以重复使用字典中的单词。
```

**示例 3：**

```
输入:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
输出:
[]
```



### 解答

​	这道题毫无疑问要用回溯算法去解了，但是又无法AC，看了评论从才知道有些特例不可分但是又很长，所以直接使用上一道题的代码判断是否可分，避免这种情况后再使用DFS搜索，结果AC。

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> List[str]:

        # 先使用动态规划判断一下是否存在可分的情况，否则特例可能会超时
        dp = [0]*(len(s)+1)
        dp[0] = 1
        for i in range(1,len(s)+1):
            for j in range(i):
                # print(s[j:i])
                if dp[j] and s[j:i] in wordDict:
                    dp[i] = 1
                    break
        res = []
        temp = []
        # 再使用回溯算法解决
        if dp[-1]:      
            self.dfs_search(s, wordDict, res, temp, 0)
        return res

    def dfs_search(self, s, wordDict, res, temp, start):
        if start == len(s):
            res.append(' '.join(temp))

        for i in range(start, len(s)):
            if s[start:i + 1] in wordDict:
                temp.append(s[start:i + 1])
                self.dfs_search(s, wordDict,res,temp,i + 1)
                temp.pop(-1)
```

