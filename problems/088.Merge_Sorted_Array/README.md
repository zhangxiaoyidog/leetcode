## 088.Merge Sorted Array

### 题目描述

给定两个有序整数数组 *nums1* 和 *nums2*，将 *nums2* 合并到 *nums1* 中*，*使得 *num1* 成为一个有序数组。

**说明:**

- 初始化 *nums1* 和 *nums2* 的元素数量分别为 *m* 和 *n*。
- 你可以假设 *nums1* 有足够的空间（空间大小大于或等于 *m + n*）来保存 *nums2* 中的元素。

**示例:**

```
输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]
```



### 解答

​	这道题如果只是合并两个数组其实很简单，但是要求合并到nums1中，也就是尽量不要使用额外的空间，仔细观察一下，在nums1中已经有了足够的空间，所以我们只需要在遍历nums1和nums2的同时从后往前去汪nums1中去填值就好了，这样就不会出现在遍历之前就修改了nums1中的元素的这种情况。

```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        i,j = m-1,n-1
        pos = m + n -1
        while i >=0 and j >= 0:
            if nums1[i] >= nums2[j]:
                nums1[pos] = nums1[i]
                i-=1
            else:
                nums1[pos] = nums2[j]
                j-=1
            pos -= 1
        
        while i>=0:
            nums1[pos] = nums1[i]
            i-=1
            pos-=1
        while j>=0:
            nums1[pos] = nums2[j]
            j-=1
            pos-=1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 