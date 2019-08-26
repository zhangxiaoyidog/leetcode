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

- 时间复杂度：$O(n+m)$
- 空间复杂度：$O(1)$



## 解答2

​	这道题要求了算法的时间复杂度为O(log(m + n))，上面的那种解法是达不到这个时间复杂度的，由于两个数组都有序，很明显，我们只有用到二分的方法才能达到，我们不妨用另一种思路，题目是求中位数，其实就是求第 `k` 小数的一种特殊情况。

​	详细的话可以看题解的第三个[解答](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-w-2/)。

```python
class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        # 奇数和偶数同时考虑
        left = (len(nums1) + len(nums2) + 1)//2
        right = (len(nums1) + len(nums2) + 2)//2
        return (self.findmedian(nums1, 0, len(nums1)-1, nums2, 0, len(nums2)-1, left) + self.findmedian(nums1, 0, len(nums1)-1, nums2, 0, len(nums2)-1, right))*0.5
    
    def findmedian(self, nums1, start1, end1, nums2, start2, end2, k):
        len1 = end1 - start1 + 1
        len2 = end2 - start2 + 1
        if len1>len2:
            return self.findmedian(nums2, start2, end2, nums1, start1, end1, k)
        
        if len1==0:
            return nums2[start2+k-1]
        
        if k==1:
            return min(nums1[start1], nums2[start2])
        
        i = start1 + min(len1, k//2)-1
        j = start2 + min(len2, k//2)-1
        
        if nums1[i]>nums2[j]:
            return self.findmedian(nums1, start1, end1, nums2, j+1, end2, k-(j-start2+1))
        else:
            return self.findmedian(nums1, i+1, end1, nums2, start2, end2, k-(i-start1+1))
```

- 时间复杂度：$O(log(n+m))$
- 空间复杂度：$O(1)$

