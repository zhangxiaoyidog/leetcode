## 031.Next Permutation

### 题目描述

实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列。

如果不存在下一个更大的排列，则将数字重新排列成最小的排列（即升序排列）。

必须**原地**修改，只允许使用额外常数空间。

以下是一些例子，输入位于左侧列，其相应输出位于右侧列。
`1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1`

### 解答

​	这道题的解决方法比较巧妙，首先是从右往左扫描如果满足前面的数字大于后面的数字则继续，否则编辑标记这个元素，如何才能排列成下一个更大的数字呢，我们需要找到被标记的元素右边的比它大的数字，所以再次从右边进行扫描，找到第一个比它大的数字替换两者，但是现在的数字并不是我们想要的下一个更大的序列，以为a[i-1]右边的序列是降序排列，所以我们需要把它倒过来，才能得到最终的结果。

```python
class Solution:
    def nextPermutation(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        i = len(nums) - 2
        while i >= 0 and nums[i + 1] <= nums[i]:
            i -= 1

        if i >= 0:
            j = len(nums) - 1
            while j >= 0 and nums[j] <= nums[i]:
                j -= 1
            self.swap(nums, i, j)

        self.reverse(nums, i + 1)

    def reverse(self, nums, start):
        i = start
        j = len(nums) - 1
        while i < j:
            self.swap(nums, i, j)
            i += 1
            j -= 1

    def swap(self, nums, i, j):
        temp = nums[i]
        nums[i] = nums[j]
        nums[j] = temp
```

- 时间复杂度：$O(n)$，在最坏的情况下，只需要对整个数组进行两次扫描。
- 空间复杂度：$O(1)$，没有使用额外的空间，原地替换足以做到。