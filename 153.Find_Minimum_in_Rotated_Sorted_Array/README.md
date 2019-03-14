## 153.Find Minimum in Rotated Sorted Array

## 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。

**示例 1:**

```
输入: [3,4,5,1,2]
输出: 1
```

**示例 2:**

```
输入: [4,5,6,7,0,1,2]
输出: 0
```

### 解答１

​	第一种解法就是直接顺序遍历，i+1位置的数字比第i个小，则找到最小值，否则一直往前遍历。

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:        
        if len(nums) == 1:
            return nums[0]
        des = nums[0]
        for i in range(1,len(nums)):
            if nums[i]<nums[i-1]:
                des = nums[i]
        return des
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$



### 解答２

​	这个题跟之前做过的一道题很相似，只不过那道题是查找某一个确定的数字，但是思想都一样，可以使用二分查找的方式找到最小元素。

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        二分查找找到分界点
        b = self.get_boundry(nums)
        # return nums[b] if nums[0] > nums[b] else nums[0]
        return nums[b]

    def get_boundry(self,s):
        
        l = 0
        r = len(s) - 1
        while l<r:
            mid = (l+r)//2
            if s[mid]>s[r]:
                l = mid + 1
            else:
                r = mid
        return l               
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$