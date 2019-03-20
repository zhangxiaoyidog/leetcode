## 014 Longest Common Prefix

### 题目描述

编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。



**示例 1:**

```
输入: ["flower","flow","flight"]
输出: "fl"
```

**示例 2:**

```
输入: ["dog","racecar","car"]
输出: ""
解释: 输入不存在公共前缀。
```

**说明:**

所有输入只包含小写字母 `a-z` 。



### 解答

​	这道题其实很简单，最容易的办法就是先找到最短的字符串，然后以它的长度为循环去对比第一个和所有的字符串的每一个字符是否相等，不相等则break，最后返回结果即可。

```python
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if len(strs) == 0:
            return ""
        strs_lens = [len(s) for s in strs]
        min_len = min(strs_lens = [len(s) for s in strs])
        flag = 0
        count = 0
        for i in range(min_len):
            for j in range(1,len(strs)):
                if strs[0][i] != strs[j][i]:
                    flag = 1
                    break
                    
            if flag == 1:
                break
            count += 1
        return strs[0][:count]
```

复杂度分析：

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n)$ （n为字符串数组大小，m为最短长度）