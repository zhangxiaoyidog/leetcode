## 016.3 Sum Closest

### 题目描述

给定一个包括 *n* 个整数的数组 `nums` 和 一个目标值 `target`。找出 `nums` 中的三个整数，使得它们的和与 `target` 最接近。返回这三个数的和。假定每组输入只存在唯一答案。

```
例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```



### 解答

​	这道题跟前面的一道题其实是一个套路，做法还是一样，首先数组排序，固定一个数，然后转化成两数之和的求法。

```python
class Solution:
    def threeSumClosest(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        nums.sort()
        if nums is None or len(nums) < 3:
            return 0
        re_tar = nums[0] + nums[1] + nums[2]
        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            start = i + 1
            end = len(nums) - 1
            while start < end:
                temp = nums[i] + nums[start] + nums[end]
                if abs(target - temp) < abs(target - re_tar):
                    re_tar = temp
                    while start < end and nums[start] == nums[start + 1]:
                        start += 1
                    while start < end and nums[end] == nums[end - 1]:
                        end -= 1
                elif temp < target:
                    start += 1
                else:
                    end -= 1
        return re_tar
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 