## 018.4 Sum 

### 题目描述

给定一个包含 *n* 个整数的数组 `nums` 和一个目标值 `target`，判断 `nums` 中是否存在四个元素 *a，b，c* 和 *d* ，使得 *a* + *b* + *c* + *d* 的值与 `target` 相等？找出所有满足条件且不重复的四元组。

**注意：**

答案中不可以包含重复的四元组。

**示例：**

```
给定数组 nums = [1, 0, -1, 0, -2, 2]，和 target = 0。

满足要求的四元组集合为：
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

### 解答

​	这道题还是采用了之前3 SUM的思路，不过这次是数组排序后，先固定两个数，然后去循环，其实套路都是差不多的，这里就不再过多赘述，只是里面的一些细节需要注意一下。

```python
class Solution:
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        nums.sort()
        re_list = []
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i + 1, len(nums)):
                if j > i+1 and nums[j] == nums[j - 1]:
                    continue
                start = j + 1
                end = len(nums) - 1
                while start < end:
                    four_sum = nums[i] + nums[j] + nums[start] + nums[end]
                    if four_sum < target:
                        start += 1
                    elif four_sum > target:
                        end -= 1
                    else:
                        re_list.append([nums[i], nums[j], nums[start], nums[end]])
                        while start < end and nums[start] == nums[start + 1]:
                            start += 1
                        while start < end and nums[end] == nums[end - 1]:
                            end -= 1
                        start += 1
                        end -= 1
        return re_list
```

复杂度分析：

- 时间复杂度：$O(n^3)$
- 空间复杂度：$O(n)$ 