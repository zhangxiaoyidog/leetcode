## 035.**Search Insert Position**

### 题目描述

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

**示例 1:**

```
输入: [1,3,5,6], 5
输出: 2
```

**示例 2:**

```
输入: [1,3,5,6], 2
输出: 1
```

**示例 3:**

```
输入: [1,3,5,6], 7
输出: 4
```

**示例 4:**

```
输入: [1,3,5,6], 0
输出: 0
```

### 解答1

​	第一种方法就是暴力搜索，代码量很少，时间复杂度高。

```python
class Solution:
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        i = 0
        while i<len(nums) and target > nums[i]:
            i+=1
        return i
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

### 解答2

​	第二种解法就是使用二分法查找要插入的位置，然后再进行插入。

```python
class Solution:
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        l = 0
        r = len(nums)
        while l < r:
            mid = (l + r) // 2
            if target <= nums[mid]:
                r = mid
            else:
                l += 1
        return l
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$