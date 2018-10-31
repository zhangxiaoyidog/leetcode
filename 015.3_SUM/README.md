## 015 3 Sum

### 题目描述

给定一个包含 *n* 个整数的数组 `nums`，判断 `nums` 中是否存在三个元素 *a，b，c ，*使得 *a + b + c =* 0 ？找出所有满足条件且不重复的三元组。

**注意：**答案中不可以包含重复的三元组。

```
例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

### 解答	

​	这道题的话可以结合之前的两数之和的解法，先把数组排序，然后固定一个数，转换成两数之和的解法，算是枚举求解吧，时间复杂度较高。

```python
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        re_list = []
        nums.sort()
        for i in range(len(nums)):
            if i>0 and nums[i] == nums[i-1]:
                continue
            start = i + 1
            end = len(nums) - 1
            while(start < end):
                if nums[i] + nums[start] + nums[end] == 0:
                    re_list.append([nums[i], nums[start], nums[end]])
                    while start<end and nums[start]==nums[start+1]:
                        start+=1
                    while start<end and nums[end]==nums[end-1]:
                        end-=1
                    start+=1
                    end-=1
                elif nums[i] + nums[start] + nums[end] < 0:
                    start+=1
                else:
                    end-=1
        return re_list
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 