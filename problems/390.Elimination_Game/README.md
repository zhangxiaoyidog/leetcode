## 390.Elimination Game

### 题目描述

给定一个从1 到 n 排序的整数列表。
首先，从左到右，从第一个数字开始，每隔一个数字进行删除，直到列表的末尾。
第二步，在剩下的数字中，从右到左，从倒数第一个数字开始，每隔一个数字进行删除，直到列表开头。
我们不断重复这两步，从左到右和从右到左交替进行，直到只剩下一个数字。
返回长度为 n 的列表中，最后剩下的数字。

示例：

```
输入:
n = 9,
1 2 3 4 5 6 7 8 9
2 4 6 8
2 6
6

输出:
6
```



### 解答

​	一开始想的就是按照题目的要求一步步消除，但是提交超时，看了discuss和网上的解答才知道需要用技巧和数学规律，是比较难的一道题目了。

```python
class Solution:
    def lastRemaining(self, n: int) -> int:
        # 超时解法
        # if n==1:
        #     return 1
        # l = [_ for _ in range(1,n+1)]
        # i = 1
        # while len(l)!=1:
        #     res = []
        #     if i%2==1:
        #         j = 1
        #         while j<len(l):
        #             res.append(l[j])
        #             j+=2
        #     else:
        #         j = len(l)-2
        #         while j>=0:
        #             res.insert(0,l[j])
        #             j-=2
        #     l = list(res)
        #     i += 1
        # return res[0]
        if n==1:
            return 1
        else:
            # print(n/2 + 1,self.lastRemaining(n/2))
            return 2*(n//2 + 1 - self.lastRemaining(n//2));
```

