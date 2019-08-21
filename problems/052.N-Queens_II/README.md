## 052.N-Queens II

### 题目描述

n 皇后问题研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/8-queens.png)

上图为 8 皇后问题的一种解法。

给定一个整数 n，返回所有不同的 n 皇后问题的解决方案的数量。



**示例:**

```
输入: 4
输出: 2
解释: 4 皇后问题存在如下两个不同的解法。
[
 [".Q..",  // 解法 1
  "...Q",
  "Q...",
  "..Q."],
  
 ["..Q.",  // 解法 2
  "Q...",
  "...Q",
  ".Q.."]
]
```



### 解答

​	这道题跟上道题不同的是要求的只是解法的数目，那么直接采用DFS求解，也就是一行一行处理，在每一行可以选择把皇后放在第n个位置，也就是每行有n中选择，只不过放好之后需要判断是否合理，也就是是否跟前面的行冲突，我们知道检查冲突的办法也就是检查行列冲突、左对角线冲突(横纵坐标之 差 相同)、右对角线冲突(横纵坐标之 和 相同)，如果合理则继续向下递归。

```python
class Solution(object):
    def totalNQueens(self, n):
        """
        :type n: int
        :rtype: int
        """
        self.res = 0
        self.queen([None]*n)
        return self.res
        
    def queen(self, A, cur=0):
        """
        :param A:
        :param cur:
        :return:
        """
        if cur == len(A):
            self.res+=1
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

