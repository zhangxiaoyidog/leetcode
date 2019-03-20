## 041.First Missing Positive

### 题目描述

给定一个未排序的整数数组，找出其中没有出现的最小的正整数。

**示例 1:**

```
输入: [1,2,0]
输出: 3
```

**示例 2:**

```
输入: [3,4,-1,1]
输出: 2
```

**示例 3:**

```
输入: [7,8,9,11,12]
输出: 1
```

**说明:**

你的算法的时间复杂度应为O(*n*)，并且只能使用常数级别的空间。



### 解答

​	这道题我感觉比较简单，直接排序数组遍历判断就可以了，采用一个游标从1开始和每个num去比较，如果相等则加一，如果大于它则break输出。

```python
class Solution:
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        nums.sort()
        i = 1
        for num in nums:
            # if num<=0
            if num > i:
                break
            if num == i:
                i += 1
        return i
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$