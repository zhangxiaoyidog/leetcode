## 367.Valid Perfect Square

### 题目描述

给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。

说明：不要使用任何内置的库函数，如  sqrt。

**示例 1：**

```
输入：16
输出：True
```


**示例 2：**

```
输入：14
输出：False
```



### 解答

​	首先这道题可以转化成是找一个不超过num的数m，使得m*m等于num，如果使用线性查找估计会超时，所以可以是能够使用二分查找的，并且有一个小trick是num的平方根肯定不会超过num//2，所以查找的范围又可以缩小，这里有一个问题，不同情况下使用二分查找的时候while循环的条件是不一样的，有时候l<=r，有时候是l<r，这个需要根据不同问题来判断。

```python
class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        #　num的平方根肯定不会超过num//2 二分查找
        if num==1 :
            return True
        l = 1
        r = num//2

        while l <= r:
            mid = (l+r)//2
            if mid*mid>num:
                r = mid-1
            elif mid*mid<num:
                l = mid + 1
            else:
                return True
        return False
```

- 时间复杂度：$O(log_2n)$
- 空间复杂度：$O(1)$ 


