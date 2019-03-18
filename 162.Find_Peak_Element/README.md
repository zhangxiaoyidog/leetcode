## 162.Find Peak Element

## 题目描述

峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 `nums`，其中 `nums[i] ≠ nums[i+1]`，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 `nums[-1] = nums[n] = -∞`。

**示例 1:**

```
输入: nums = [1,2,3,1]
输出: 2
解释: 3 是峰值元素，你的函数应该返回其索引 2。
```

**示例 2:**

```
输入: nums = [1,2,1,3,5,6,4]
输出: 1 或 5 
解释: 你的函数可以返回索引 1，其峰值元素为 2；
     或者返回索引 5， 其峰值元素为 6。
```

**说明:**

你的解法应该是 *O*(*logN*) 时间复杂度的。



### 解答

​	要求时间复杂度为O(logN)，那么肯定是要用二分法去解题的，这里不是排序数组，如何让用二分法呢，如果nums[i] > nums[i+1]，则在i之前一定存在峰值元素，如果nums[i] < nums[i+1]，则在i+1之后一定存在峰值元素，依照这个规律，即可使用二分查找了。

```python
class Solution(object):
    def findPeakElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 要求logN,要用二分查找
        if len(nums)==1 or nums[1]<nums[0]:
            return 0
        if nums[-1]>nums[-2]:
            return len(nums)-1

        l = 0
        r = len(nums) - 1 
        while l < r:
            mid = (l+r)//2
            if nums[mid-1] < nums[mid] > nums[mid+1]:
                return mid
            # 峰值在左边
            elif nums[mid-1] > nums[mid]:
                r = mid
            # 峰值在右边
            else:
                l = mid
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$

