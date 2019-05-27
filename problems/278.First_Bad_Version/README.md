## 278.First Bad Version

## 题目描述

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 `n` 个版本 `[1, 2, ..., n]`，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 `bool isBadVersion(version)` 接口来判断版本号 `version` 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

**示例:**

```
给定 n = 5，并且 version = 4 是第一个错误的版本。

调用 isBadVersion(3) -> false
调用 isBadVersion(5) -> true
调用 isBadVersion(4) -> true

所以，4 是第一个错误的版本。 
```



### 解答

​	这道题还是使用二分查找，说到底是寻找边界的问题，也就是找到第一个True，假如有序列
FFFTT，那么我们直接使用二分查找即可 ，假如mid为F那么答案在右边，反之在左边。

```python
# The isBadVersion API is already defined for you.
# @param version, an integer
# @return a bool
# def isBadVersion(version):

class Solution:
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        l = 1
        r = n
        # 二分查找
        
        while l<r:
            mid = (l + r)//2
            if isBadVersion(mid):
                r = mid
            else:
                l = mid+1
        return l
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$ 