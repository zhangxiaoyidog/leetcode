## 440.K-th Smallest in Lexicographical Order

## 题目描述

给定整数 n 和 k，找到 1 到 n 中字典序第 k 小的数字。

注意：1 ≤ k ≤ n ≤ 109。

**示例 :**

```
输入:
n: 13   k: 2

输出:
10

解释:
字典序的排列是 [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9]，所以第二小的数字是10。
```



### 解答

​	这道题比较难，需要把字典排序转化成一个十叉树来做，采用先序遍历的方法就可以找到第k个值了，但是这里看了答案有一个小技巧可以减少遍历的时间，也就是判断两个相差为1的数字之间隔了几个数字，如果比k小，那么直接跳过来不用再遍历这之间的数字了。

![](https://note.youdao.com/yws/api/personal/file/WEB4b1f87f317f0fa6fb8d5c4cb74f9bd4f?method=download&shareKey=81505dc6dc32fa00952ca2a87b40c222)

```python
class Solution:
    def findKthNumber(self, n: int, k: int) -> int:
        cur = 1
        k -= 1
        while k>0:
            step = self.cal(n, cur, cur+1)
            if step<=k:
                cur+=1
                k-=step
            else:
                cur*=10
                k-=1
        return cur
    
    def cal(self,n, n1, n2):
        """
        计算两个相差为1的数字之间的距离
        """
        step = 0
        while n1 <= n:
            step += min(n + 1, n2) - n1
            n1 *= 10
            n2 *= 10
        return step
```

