## 033.Search in Rotated Sorted Array

### 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 `-1` 。

你可以假设数组中不存在重复的元素。

你的算法时间复杂度必须是 *O*(log *n*) 级别。

**示例 1:**

```
输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
```

**示例 2:**

```
输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```

### 解答

​	这道题可以使用暴力搜索，但是题目要求算法的时间复杂度必须是 *O*(log *n*) 级别。所以看到这里自然就得想到二分法查找，所以可以先使用二分法找到中界点，也就是后半段的起始点，然后分别在前半段和后半段使用二分查找去寻找结果。

```python
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """

        b = self.find_boundary(nums)
        # 1.在前半段找target

        find_r = self.binary_search(nums[:b], target)
        if find_r == -1:
            # 2.在后半段找target
            find_r = self.binary_search(nums[b:], target)
            if find_r != -1:
                find_r+=b
        return find_r if find_r != -1 else -1



    def find_boundary(self, s):
        """
        # 二分法找到中界点
        :type s: list[int]
        :rtype: int
        """
        l = 0
        r = len(s) - 1
        while l < r:
            mid = (l + r) // 2
            if s[mid] > s[r]:
                l = mid + 1
            else:
                r = mid
        return l
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$



### 解答3 

​	今天在面试作业帮遇到了这个题，我答的是第二种，结果面试官说不可以这样，经过提示才知道这种解法，实在是很难受，刷题要认真。

​	其实不用两遍二分查找，每次得到mid后，先判断l-mid是否有序，假如有序，分两种情况，target在左边和在右边，假如右边有序，也是同样的两种情况。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if len(nums)==0:
            return -1
        l, r = 0, len(nums)-1
        while l<r:
            mid = l + (r - l)//2
            # 左边有序
            if nums[mid]>=nums[l]:
                # target在左边
                if nums[l]<= target <=nums[mid]:
                    r = mid
                else:
                    l = mid + 1
            else:
                # target在右边
                if nums[mid]<= target <=nums[r]:
                    l = mid
                else:
                    r = mid -1
        return l if nums[l]==target else -1
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$