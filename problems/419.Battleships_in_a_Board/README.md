## 419.Partition Equal Subset Sum

## 题目描述

给定一个二维的甲板， 请计算其中有多少艘战舰。 战舰用 'X'表示，空位用 '.'表示。 你需要遵守以下规则：

+ 给你一个有效的甲板，仅由战舰或者空位组成。
+ 战舰只能水平或者垂直放置。换句话说,战舰只能由 1xN (1 行, N 列)组成，或者 Nx1 (N 行, 1 列)组成，其中N可以是任意大小。
+ 两艘战舰之间至少有一个水平或垂直的空位分隔 - 即没有相邻的战舰。

**示例 :**

```
X..X
...X
...X
```

在上面的甲板中有2艘战舰。

**无效样例 :**

```
...X
XXXX
...X
```

你不会收到这样的无效甲板 - 因为战舰之间至少会有一个空位将它们分开。

**进阶:**

你可以用一次扫描算法，只使用O(1)额外空间，并且不修改甲板的值来解决这个问题吗？



### 解答

​	由于不会有无效夹板，也就是可以直接判断上面和左边是否有空位即可。

```python
class Solution:
    def countBattleships(self, board: List[List[str]]) -> int:
        count = 0
        for i in range(len(board)):
            for j in range(len(board)):
                if board[i][j]=='X':
                    flag = 1
                    if i!=0 and board[i-1][j]=='X':
                        flag=0
                    if j!=0 and board[i][j-1]=='X':
                        flag=0
                    if flag:
                        count+=1
        return count
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$