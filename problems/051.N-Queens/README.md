## 051.N-Queens

### 题目描述

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/8-queens.png)

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案。

每一种解法包含一个明确的 n 皇后问题的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

**示例:**

```
输入: 4
输出: [
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],
  
 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
解释: 4 皇后问题存在两个不同的解法。
```



### 解答

​	建议先看一下[52](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/052.N-Queens_II/README.md)，使用的是一样的方法，只不过这道题需要把解法都输出出来，那么只需要在得到结果那一步修改一下即可，也就是把当前输出结果生成需要的格式即可。

```python
class Solution(object):
    def solveNQueens(self, n):
        """
        :type n: int
        :rtype: List[List[str]]
        """
        self.res = []
        self.queen([None]*n)
        return self.res
        
    def queen(self, A, cur=0):
        """
        :param A:
        :param cur:
        :return:
        """
        if cur == len(A):
            temp = []
            for line in A:
                l = ['.']*len(A)
                l[line] = 'Q'
                temp.append(''.join(l))
            self.res.append(temp)
        else:
            for col in range(len(A)):
                # 把第cur行的皇后放到col列
                A[cur] = col
                flag = 1
                for r in range(cur):
                    if A[r] == col or r + A[r] == cur + A[cur] or r - A[r] == cur - A[cur]:
                        flag = 0
                        break
                if flag:
                    self.queen(A, cur + 1)
```




