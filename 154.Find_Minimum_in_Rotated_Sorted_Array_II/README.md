## 154.Find Minimum in Rotated Sorted Array II

## 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

请找出其中最小的元素。

注意数组中可能存在重复的元素。

**示例 1：**

```
输入: [1,3,5]
输出: 1
```

**示例 2：**

```
输入: [2,2,2,0,1]
输出: 0
```

**说明：**

- 这道题是 [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/description/) 的延伸题目。
- 允许重复会影响算法的时间复杂度吗？会如何影响，为什么？



### 解答

​	这道题我也是采用了二分查找的方法，不过这里的由于有重复值的情况，需要加入 mid 元素等于r元素的情况，此时应该将r减1防止重复数字是最小元素。之前的那个题没想到这一点，也就是[2,2,2,0,2,2]的这种情况，如果使用上道题的写法是找不到分界点的。

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        # 二分法
        l = 0
        r = len(nums) -1 
        while l<r:
            mid = (l + r)//2
            if nums[mid]>nums[r]:
                l = mid+1
            elif nums[mid]<nums[r]:
                r = mid
            else:
                r-=1
        return nums[l]
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$