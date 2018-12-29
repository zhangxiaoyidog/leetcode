## 079.Word Search

### 题目描述

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

**示例:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true.
给定 word = "SEE", 返回 true.
给定 word = "ABCB", 返回 false.
```



### 解答

​	这道题也是需要使用上一道题讨论过的DFS，以每一个点作为深度搜索的起点，可以向左，可以向右，可以向上也可以向下，这里要控制好边界条件以及不能重复访问，若存在一种路径和word相同，直接返回True，这种问题做的还是比较少，所以写起代码还是有些不熟悉，要注意总结提高。

```python
class Solution:
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """

        def dfs_all(board, word, step, row, col):
            if board[row][col] != word[step]:
                return False
            if step == len(word) - 1:
                return True
            # 表示这一轮不能再重复使用了
            visited[row][col] = 1
            for move in moves:
                r = row + move[0]
                c = col + move[1]
                if r < 0 or r >= m or c < 0 or c >= n or visited[r][c] == 1:
                    continue
                if dfs_all(board, word, step + 1, r, c):
                    return True
            visited[row][col] = 0
            return False

        if len(board) == 0 or len(board[0]) == 0:
            return False
        if len(word) == 0:
            return True
        m = len(board)
        n = len(board[0])
        moves = [[-1, 0], [1, 0], [0, 1], [0, -1]]
        visited = [[0 for q in range(n)] for p in range(m)]

        # dfs寻找每种可能去比较，相等就返回true
        for i in range(m):
            for j in range(n):
                if dfs_all(board, word, 0, i, j):
                    return True
        return False
```

