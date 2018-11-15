## 034.Search For a Range

### 题目描述

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 *O*(log *n*) 级别。

如果数组中不存在目标值，返回 `[-1, -1]`。

**示例 1:**

```
输入: nums = [5,7,7,8,8,10], target = 8
输出: [3,4]
```

**示例 2:**

```
输入: nums = [5,7,7,8,8,10], target = 6
输出: [-1,-1]
```

### 解答1

这道题的思路大概和上道题有些相似，首先利用2分法找到一个target的位置，然后从这个位置往两边寻找边界，最后返回这个范围。

```python
class Solution:
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        
        pos = self.binary_search(nums,target)
        if pos==-1:
            return [-1,-1]
        l = r = pos
        while l>0 and nums[l-1]==nums[pos]:
            l-=1
        while r<len(nums)-1 and nums[r+1]==nums[pos]:
            r+=1
        return [l,r]
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
```

- 时间复杂度：$O(n)$（因为最后向两边寻找，所以最坏的情况下会出现O(n)的情况）
- 空间复杂度：$O(1)$

### 解答2

​	还是使用二分查找，但是这次是用两次二分查找，第一次找上边界，第二次找下边界，微调代码即可实现。

```python
class Solution:
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        l = 0
        r = len(nums) - 1
        while l < r:
            mid = (l + r) // 2
            if nums[mid] >= target:
                r = mid
            else:
                l = mid + 1
        if l==len(nums) or nums[l]!=target:
            return [-1,-1]
        start = l
        l = 0
        r = len(nums) - 1
        while l < r:
            mid = (l + r) // 2 + 1
            if nums[mid] <= target:
                l = mid
            else:
                r = mid - 1
        end = r
        return [start,end]
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$

