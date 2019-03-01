## 131.Palindrome Partitioning

## 题目描述

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回 *s* 所有可能的分割方案。

**示例:**

```
输入: "aab"
输出:
[
  ["aa","b"],
  ["a","a","b"]
]
```



### 解答

​	这道题我是做了[132](https://github.com/zhangxiaoyidog/leetcode/blob/master/132.Palindrome_Partitioning II/README.md)题才有的思路，首先利用动态规划求出第i个位置到第j个位置是否为回文串，然后使用回溯算法，递归寻找符合的分割方案，也就是使用之前的模板。具体细节看代码。

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        # isPal[i][j]表示i到j是否是回文串
        isPal = [[0]*len(s) for i in range(len(s))]
        for j in range(len(s)):
            for i in range(j+1):
                if s[i]==s[j] and (j-i<3 or isPal[i+1][j-1]==1):
                    isPal[i][j]=1
        
        # 接下来使用回溯模板解决
        res = []
        temp = []
        self.dfs_sreach(s,res,temp,isPal,0)
        return res
    def dfs_sreach(self,s,res,temp,isPal,l):
        if l == len(s):
            res.append(list(temp))
            return
        for i in range(l,len(s)):
            if isPal[l][i]:
                temp.append(s[l:i+1])
                self.dfs_sreach(s,res,temp,isPal,i+1)
                # 这里不能用remove，因为可能会删掉其他位置的同样的字符，提交就报错
                temp.pop(-1)
```

