## 069.Sqrt(x)

### 题目描述

实现 `int sqrt(int x)` 函数。

计算并返回 *x* 的平方根，其中 *x* 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

**示例 1:**

```
输入: 4
输出: 2
```

**示例 2:**

```
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```

### 解答1

​	最容易想到的就是使用暴力法从0搜索到x/2，但是这里的返回条件要限定，具体看代码部分，但是这个提示没法AC，因为超出内存限制了。

```python
class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        if x<=1:
            return x
        
        for i in range(x//2+1):
            if i*i<=x and (i+1)*(i+1)>x:
                return i
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

### 解答2

​	这个问题归根结底也就是一个搜索问题，对了！我们最常使用的搜索算法难道不是2分查找吗？这样时间复杂度也会降低，也不会遍历到很大的数。

```python
class Solution(object):
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        low = 0
        high = x
        while low <=high:
            mid = (low+high)//2
            if mid*mid<=x:
                ans = mid
                low = mid + 1
            else:
                high = mid-1
        return ans
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$ 