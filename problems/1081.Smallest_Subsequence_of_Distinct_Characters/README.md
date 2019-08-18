## 1081.Smallest Subsequence of Distinct Characters

## 题目描述

返回字符串 text 中按字典序排列最小的子序列，该子序列包含 text 中所有不同字符一次。

 

**示例 1：**

```
输入："cdadabcc"
输出："adbc"
```

**示例 2：**

```
输入："abcd"
输出："abcd"
```

**示例 3：**

```
输入："ecbacba"
输出："eacb"
```

**示例 4：**

```
输入："leetcode"
输出："letcod"
```


**提示：**

1. 1 <= text.length <= 1000
2. text 由小写英文字母组成



### 解答

​	一开始我的想法是遍历过程中当前字母如果不存在于res中，那么就往里面添加，如果存在那么判断res中它存在的位置后面一个或者后面所有的字母是否小于它如果小于则弹出重新添加，但是这样有用例是过不了的，比如"ddeeeccdce"和"leetcode"，需要另辟蹊径，所以正确的做法应该是使用贪心的策略，遇到一个新的字母，我要看**已经出现过的字符将来还有没有可能出现，如果将来有可能出现，就把前面的字符依次删去**，经过这样的流程，得到的子序列就符合题意。

```python
class Solution(object):
    def smallestSubsequence(self, text):
        """
        :type text: str
        :rtype: str
        """
        res = []
        for i in range(len(text)):
            if text[i] in res:
                continue
            while res and text[i] < res[-1] and text.find(res[-1], i) != -1:
                res.pop(-1)
            res.append(text[i])
        return ''.join(res)
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$