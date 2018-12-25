## 072.Edit Distance

### 题目描述

给定两个单词 *word1* 和 *word2*，计算出将 *word1* 转换成 *word2* 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

1. 插入一个字符
2. 删除一个字符
3. 替换一个字符

**示例 1:**

```
输入: word1 = "horse", word2 = "ros"
输出: 3
解释: 
horse -> rorse (将 'h' 替换为 'r')
rorse -> rose (删除 'r')
rose -> ros (删除 'e')
```

**示例 2:**

```
输入: word1 = "intention", word2 = "execution"
输出: 5
解释: 
intention -> inention (删除 't')
inention -> enention (将 'i' 替换为 'e')
enention -> exention (将 'n' 替换为 'x')
exention -> exection (将 'n' 替换为 'c')
exection -> execution (插入 'u')
```

### 解答

​	这道题需要用动态规划来帮助解题的，首先还是解决关键问题--如何定义状态转移数组，做了一些动态规划的题目，我发现大部分的题目的动态转移数组最终都是直观地反映题目的返回值，所以在这个问题中，我们定义`D[i][j]`为长度为`i`的字符串X和长度为`j`的字符串Y的最小编辑距离，我们要求解的就是最终的状态`D[m][n]`，然后去定义边界值，由于这道题是把word1变为word2，所以边界有两种情况，一是word1为空，则直接不断插入就好，即dp\[i][0]=i,二是word2为空，则不断去删除word1中的字母即可，即dp\[0][i]=i。最后我们要做的就是找到动态转移方程了，一般这种题目当前状态肯定是与前面的状态有关的，看下图可以分为三种情况，第一种是蓝色情况，这种即word1比word2少一个字母，插入即可，第二种为红色情况，这时需要删除word1中的元素，第三种比较不容易分析，也就是黄色情况，这时候需要判断i和j位置的字母是否相同来决定是否替换，最终的转移值等于这三种情况的最小值。具体细节可以看代码。

![img](https://camo.githubusercontent.com/e9dccce2aeef3d06c1af19971120337f7b9156ee/687474703a2f2f75706c6f61642d696d616765732e6a69616e7368752e696f2f75706c6f61645f696d616765732f393337313838372d343362333464623038633262313732392e706e673f696d6167654d6f6772322f6175746f2d6f7269656e742f7374726970253743696d61676556696577322f322f772f373030)



```python
class Solution:
    def minDistance(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        # 动态规划解题 dp[m][n]表示word1长度为m，word2长度为n时使用的最少操作数
        dp = [[0 for i in range(len(word1) + 1)] for j in range(len(word2) + 1)]
        print(dp)
        # 边界
        if len(word1) == 0:
            return len(word2)
        if len(word2) == 0:
            return len(word1)
        # word2为空 word1做删除操作
        for i in range(len(word1) + 1):
            dp[0][i] = i
        # word1为空 word1做插入操作
        for j in range(len(word2) + 1):
            dp[j][0] = j

        for i in range(1, len(word2) + 1):
            for j in range(1, len(word1) + 1):
                insert = dp[i][j-1] + 1
                delete = dp[i-1][j] + 1
                if word1[j - 1] != word2[i - 1]:
                    replace = dp[i - 1][j - 1] + 1
                else:
                    replace = dp[i - 1][j - 1]
                dp[i][j] = min(insert, delete, replace)
        return dp[len(word2)][len(word1)]
```

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n*m)$ 