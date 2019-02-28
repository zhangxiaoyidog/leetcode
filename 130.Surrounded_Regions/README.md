## 130.Surrounded Regions

## 题目描述

给定一个二维的矩阵，包含 `'X'` 和 `'O'`（**字母 O**）。

找到所有被 `'X'` 围绕的区域，并将这些区域里所有的 `'O'` 用 `'X'` 填充。

**示例:**

```
X X X X
X O O X
X X O X
X O X X
```

运行你的函数后，矩阵变为：

```
X X X X
X X X X
X X X X
X O X X
```

**解释:**

被围绕的区间不会存在于边界上，换句话说，任何边界上的 `'O'` 都不会被填充为 `'X'`。 任何不在边界上，或不与边界上的 `'O'` 相连的 `'O'` 最终都会被填充为 `'X'`。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。



### 解答

​	这道题的解法要换一种思考方式，不要想着怎么把连通区域找到，反而是想怎么把连通边界找到，把边界‘O’的最大连通分量找到并全部标记，剩下的'O'直接转换为'X'就ok了。

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if len(board)<3:
            return
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j]=='O' and (i==0 or i==len(board)-1 or j==0 or j==len(board[0])-1):
                    self.dfs(board,i,j,len(board),len(board[0]))
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j]=='O':
                    board[i][j] = 'X'
                if board[i][j]=='1':
                    board[i][j]='O'
            
    def dfs(self, board, ix, iy, m, n):
        # DFS找到’O‘的最大连通分量
        dx = [0,0,1,-1]
        dy = [1,-1,0,0]
        board[ix][iy] = '1'
        
        for i in range(4):
            if ix+dx[i]>=0 and ix+dx[i]<m and iy+dy[i]>=0 and iy+dy[i]<n and board[ix+dx[i]][iy+dy[i]]=='O':
                self.dfs(board, ix+dx[i], iy+dy[i], m, n)
```

