## 004 Median of two sorted arrays

### 题目描述

给定两个大小为 m 和 n 的有序数组 **nums1** 和 **nums2** 。

请找出这两个有序数组的中位数。要求算法的时间复杂度为 O(log (m+n)) 。

你可以假设 **nums1** 和 **nums2** 不同时为空。

**示例:**

```python
示例 1:

nums1 = [1, 3]
nums2 = [2]

中位数是 2.0

示例 2:

nums1 = [1, 2]
nums2 = [3, 4]

中位数是 (2 + 3)/2 = 2.5

```

## 解答1

​	这道题我的想法是先把两个数组合并成同一个数组，并且合并后的数组是有序的，即使用归并排序的思想排序，最后在根据排序后的这个数组输出中位数。

```python
class Solution:
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        total_nums = []
        i = 0
        j = 0
        while i<len(nums1) and j < len(nums2):
            if nums1[i] <=nums2[j]:
                total_nums.append(nums1[i])
                i+=1
            else:
                total_nums.append(nums2[j])
                j+=1
        if i < len(nums1):
            total_nums.extend(nums1[i:len(nums1)])
        if j < len(nums2):
            total_nums.extend(nums2[j:len(nums2)])
        if len(total_nums)%2:
            return total_nums[len(total_nums)//2]
        else:
            return (total_nums[len(total_nums)//2] + total_nums[len(total_nums)//2-1])/2
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$



## 解答2

