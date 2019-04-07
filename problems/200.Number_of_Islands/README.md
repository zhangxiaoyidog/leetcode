## 200.Number Of Islands

## 题目描述

给定一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。

**示例 1:**

```
输入:
11110
11010
11000
00000

输出: 1
```

**示例 2:**

```
输入:
11000
11000
00100
00011

输出: 3
```



### 解答

​	这道题典型的使用dfs来做，之前有一个类似的题目忘了是哪个了，大概的做法就是假如此网格为'1'，那么就往4个方向去遍历，并且把这个网格置为'0'，其实也就是找到最大连接子图，统计最大连接子图的数目而已。

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        res = 0
        # dfs求解
        for m in range(len(grid)):
            for n in range(len(grid[0])):
                if grid[m][n]=='1':
                    self.dfs_search(grid,m,n)
                    res+=1
        return res
    
    def dfs_search(self,grid,m,n):
        if m<0 or n<0 or m>len(grid)-1 or n>len(grid[0])-1 or grid[m][n]=='0':
            return
        grid[m][n] = '0'
        self.dfs_search(grid,m+1,n)
        self.dfs_search(grid,m-1,n)
        self.dfs_search(grid,m,n+1)
        self.dfs_search(grid,m,n-1)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 