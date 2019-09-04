## 081.Search in Rotated Sorted Array II

### 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,0,1,2,2,5,6]` 可能变为 `[2,5,6,0,0,1,2]` )。

编写一个函数来判断给定的目标值是否存在于数组中。若存在返回 `true`，否则返回 `false`。

**示例 1:**

```
输入: nums = [2,5,6,0,0,1,2], target = 0
输出: true
```

**示例 2:**

```
输入: nums = [2,5,6,0,0,1,2], target = 3
输出: false
```

### 解答1

​	 首先这道题和33题很相似，33题我们的解法是先用一个二分搜索去寻找分界点，然后再用两个二分搜索分段查找target，但是这里的nums可能包含重复元素，在一些特殊情况使用二分搜索是找不到分界点的，这里读者可以自己尝试一下，所以我只能先使用顺序遍历找到分界点，然后在分段使用二分查找。

```python
class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: bool
        """
        b = 0
        # 找中界点
        for i in range(1,len(nums)):
            if nums[i]>=nums[b]:
                b = i
            else:
                b+=1
                break
        
        re = self.search_binary(nums[:b],target)
        if re == -1:
            re = self.search_binary(nums[b:],target)
        return True if re!=-1 else False
        
    def search_binary(self,nums,target):
        # 二分查找
        l = 0
        r = len(nums) - 1
        while l<=r:
            mid = (l+r)//2
            if nums[mid] > target:
                r = mid - 1 
            elif nums[mid] < target:
                l = mid + 1
            else:
                return mid
        return -1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	还是和第33题目一样的解法，一遍二分搜索解决。

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        if len(nums)==0:
            return False
        l, r = 0, len(nums)-1
        while l<r:
            mid = l + (r - l) // 2
            # 左边有序
            if nums[mid]>nums[l]:
                # target在左边
                if nums[l]<= target <=nums[mid]:
                    r = mid
                else:
                    l = mid + 1
            elif nums[mid]<nums[l]:
                # target在右边
                if nums[mid]<= target <=nums[r]:
                    l = mid
                else:
                    r= mid-1
            else:
                # [1,3,1,1,1] 3
                if nums[l]==target:
                    return True
                l+=1
                    
        # 后处理，夹逼以后，还要判断一下，是不是 target
        return nums[l] == target 
```

- 时间复杂度：$O(logn)$
- 空间复杂度：$O(1)$ 

