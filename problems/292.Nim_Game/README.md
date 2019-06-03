## 292.Nim Game

## 题目描述

你和你的朋友，两个人一起玩 [Nim 游戏](https://baike.baidu.com/item/Nim%E6%B8%B8%E6%88%8F/6737105)：桌子上有一堆石头，每次你们轮流拿掉 1 - 3 块石头。 拿掉最后一块石头的人就是获胜者。你作为先手。

你们是聪明人，每一步都是最优解。 编写一个函数，来判断你是否可以在给定石头数量的情况下赢得游戏。

**示例:**

```
输入: 4
输出: false 
解释: 如果堆中有 4 块石头，那么你永远不会赢得比赛；
     因为无论你拿走 1 块、2 块 还是 3 块石头，最后一块石头总是会被你的朋友拿走。
```



### 解答

​	这题需要找出其中的规律，因为两个人都是全知视角，假如最后只剩不到4块石头，那么你必胜，假如有4块必然输，再假如有5,6,7块石头，那可以刚好给对手留4块，这样必胜，假如有8块那对手肯定给你留4块，必然输，再往上也是一样的道理，这里就可以看出来了，假如有4的倍数，那就必输无疑。

```python
class Solution:
    def canWinNim(self, n: int) -> bool:
        return n%4!=0
```

- 时间复杂度：$O(1)$
- 空间复杂度：$O(1)$ 