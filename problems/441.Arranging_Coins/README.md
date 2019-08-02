## 441.Arranging Coins

## 题目描述

你总共有 n 枚硬币，你需要将它们摆成一个阶梯形状，第 k 行就必须正好有 k 枚硬币。

给定一个数字 n，找出可形成完整阶梯行的总行数。

n 是一个非负整数，并且在32位有符号整型的范围内。

**示例 1:**

```
n = 5

硬币可排列成以下几行:
¤
¤ ¤
¤ ¤

因为第三行不完整，所以返回2.
```

**示例 2:**

```
n = 8

硬币可排列成以下几行:
¤
¤ ¤
¤ ¤ ¤
¤ ¤
因为第四行不完整，所以返回3.
```



### 解答1

​	最容易想到的是直接一行行去遍历，找到第n个硬币所在的那一行即可。

```python
class Solution:
    def arrangeCoins(self, n: int) -> int:
        # 写法1
        total = 1
        line = 1
        while total < n:
            line+=1
            total+=line
        if total==n:
            return line
        else:
            return line-1
        
        # 写法2
        # line = 1
        # while line<=n:
        #     n-=line
        #     line+=1
        # return line-1
```



### 解答2

​	这个问题说到底还是一个查找的题目，并且有序，是的，其实可以转化为在1-n//2+1行去找到第n个数字在哪一行的问题，所以可以用二分查找啦。

```python
class Solution:
    def arrangeCoins(self, n: int) -> int:
        # 二分查找
        down = 0
        up = n//2+1
        while down < up:
            mid = down + (up-down)//2
            
            if n-(1+mid)*mid//2>=mid+1:
                down = mid+1
            else:
                up = mid
        return down
```

