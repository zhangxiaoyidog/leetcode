## 397.Integer Replacement

### 题目描述

给定一个正整数 n，你可以做如下操作：

1. 如果 n 是偶数，则用 n / 2替换 n。
2. 如果 n 是奇数，则可以用 n + 1或n - 1替换 n。
  n 变为 1 所需的最小替换次数是多少？

**示例 1:**

```
输入:
8

输出:
3

解释:
8 -> 4 -> 2 -> 1
```




**示例 2:**

```
输入:
7

输出:
4

解释:
7 -> 8 -> 4 -> 2 -> 1

或
7 -> 6 -> 3 -> 2 -> 1

```



### 解答

​	这道题其实有点贪心的思想在里面，因为在是奇数的时候，你需要判断是加一好还是减一好呢？换一种思考方式，减法总没除法来得快，所以在奇数判断的时候只需要判断加一后和减一后得到的两个数字除以2得到的数字能否可以被2整除，也就是做两步运算，这样可以得到局部最优。为什么要这样呢，比如1025，减去1比加1好，反之1023加一好，但是这样对于3这个特殊值需要单独处理。

```python
class Solution:
    def integerReplacement(self, n: int) -> int:
        res = 0
        if n==1:
            return res
        # print(n)
        if n==3:
            return 2
        if n%2==0:
            return 1+self.integerReplacement(n//2)
        else:
            if ((n+1)//2)%2==0:
                return 1+self.integerReplacement(n+1)
            else:
                return 1+self.integerReplacement(n-1)
```

