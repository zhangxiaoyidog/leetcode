## 374.Guess Number Higher or Lower

### 题目描述

我们正在玩一个猜数字游戏。 游戏规则如下：
我从 1 到 n 选择一个数字。 你需要猜我选择了哪个数字。
每次你猜错了，我会告诉你这个数字是大了还是小了。
你调用一个预先定义好的接口 guess(int num)，它会返回 3 个可能的结果（-1，1 或 0）：

```
-1 : 我的数字比较小
 1 : 我的数字比较大
 0 : 恭喜！你猜对了！
```

**示例 :**

```
输入: n = 10, pick = 6
输出: 6
```



### 解答

​	这道题也就是在1-n中找一个数字，这就最基本的二分查找就完事了。

```python
# The guess API is already defined for you.
# @param num, your guess
# @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
# def guess(num):

class Solution(object):
    def guessNumber(self, n):
        """
        :type n: int
        :rtype: int
        """
        l = 1 
        r = n
        # 二分查找
        while l<=r:
            mid = l+(r-l)//2
            if guess(mid)==-1:
                r=mid-1
            elif guess(mid)==1:
                l=mid+1
            else:
                return mid
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$ 