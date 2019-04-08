## 202.Happy Number

## 题目描述

编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

**示例:** 

```
输入: 19
输出: true
解释: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```



### 解答	

​	这道题直接用除数取余法来求平方和，用一个set去记录已经得到的数字，循环跳出的条件就是又得到了一个set中存在的数字。

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        if n==1:
            return True
        s = set()
        while n not in s:
            s.add(n)
            res = 0
            while n>0:
                res += (n%10)*(n%10)
                n //=10
            if res == 1:
                return True
            else:
                n = res
        return False
```

