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

    def binary_search(self, nums, target):
        l = 0
        r = len(nums) - 1
        flag = 0
        while l <= r:
            mid = (l + r) // 2
            if nums[mid] > target:
                r = mid - 1
            elif nums[mid] < target:
                l = mid + 1
            else:
                flag = 1
                break
        return mid if flag == 1 else -1

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