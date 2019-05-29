## 289.Game if Life

## 题目描述

根据[百度百科](https://baike.baidu.com/item/%E7%94%9F%E5%91%BD%E6%B8%B8%E6%88%8F/2926434?fr=aladdin)，生命游戏，简称为生命，是英国数学家约翰·何顿·康威在1970年发明的细胞自动机。

给定一个包含 m × n 个格子的面板，每一个格子都可以看成是一个细胞。每个细胞具有一个初始状态 *live*（1）即为活细胞， 或 *dead*（0）即为死细胞。每个细胞与其八个相邻位置（水平，垂直，对角线）的细胞都遵循以下四条生存定律：

1. 如果活细胞周围八个位置的活细胞数少于两个，则该位置活细胞死亡；
2. 如果活细胞周围八个位置有两个或三个活细胞，则该位置活细胞仍然存活；
3. 如果活细胞周围八个位置有超过三个活细胞，则该位置活细胞死亡；
4. 如果死细胞周围正好有三个活细胞，则该位置死细胞复活；

根据当前状态，写一个函数来计算面板上细胞的下一个（一次更新后的）状态。下一个状态是通过将上述规则同时应用于当前状态下的每个细胞所形成的，其中细胞的出生和死亡是同时发生的。

**示例:**

```
输入: 
[
  [0,1,0],
  [0,0,1],
  [1,1,1],
  [0,0,0]
]
输出: 
[
  [0,0,0],
  [1,0,1],
  [0,1,1],
  [0,1,0]
]
```

**进阶:**

- 你可以使用原地算法解决本题吗？请注意，面板上所有格子需要同时被更新：你不能先更新某些格子，然后使用它们的更新后的值再更新其他格子。
- 本题中，我们使用二维数组来表示面板。原则上，面板是无限的，但当活细胞侵占了面板边界时会造成问题。你将如何解决这些问题？



### 解答

​	这道题没有很难，也就是几个点想清楚就好，要求不能使用额外空间，所以在改变细胞状态时不能影响下一个细胞状态的判断，因此可以先把改变的状态变成其他的数字区分一下，这里我是使用了`活细胞->死细胞 2 死细胞->活细胞 -1`，最后再变为最终结果。

```python
class Solution:
    def gameOfLife(self, board: List[List[int]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        def judge(value):
            return 1 if value>0 else 0
        def count_surround(board,i,j):
            count = 0
            # 上面
            if i>0:
                count+=judge(board[i-1][j])
                if j>0:
                    count+=judge(board[i-1][j-1])
                if j<len(board[0])-1:
                    count+=judge(board[i-1][j+1])
            # 下面
            if i<len(board)-1:
                count+=judge(board[i+1][j])
                if j>0:
                    count+=judge(board[i+1][j-1])
                if j<len(board[0])-1:
                    count+=judge(board[i+1][j+1])
            
            # 左右
            if j>0:
                count+=judge(board[i][j-1])
            if j<len(board[0])-1:
                count+=judge(board[i][j+1])
            return count
        
        # 活细胞->死细胞 2 死细胞->活细胞 -1
        
        for i in range(len(board)):
            for j in range(len(board[0])):
                count = count_surround(board,i,j)
                if board[i][j] == 0:
                    if count==3:
                        board[i][j] = -1
                if board[i][j] == 1:
                    if count>3 or count<2:
                        board[i][j] = 2
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == -1:
                    board[i][j] = 1
                if board[i][j] == 2:
                    board[i][j] = 0
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 

