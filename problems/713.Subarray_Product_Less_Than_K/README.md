## 713.Subarray Product Less Than K

## 题目描述

给定一个正整数数组 nums。

找出该数组内乘积小于 k 的连续的子数组的个数。

**示例 1:**

```
输入: nums = [10,5,2,6], k = 100
输出: 8
解释: 8个乘积小于100的子数组分别为: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]。
需要注意的是 [10,5,2] 并不是乘积小于100的子数组。
```


**说明:**

+ 0 < nums.length <= 50000

+ 0 < nums[i] < 1000

+ 0 <= k < 10^6



### 解答

​	这道题是面试作业帮的时候面试官出的一道题，当时自己写的代码很冗余，其实还是使用滑动窗口的思想，假如窗口内所有数字乘积都小于k，那么这一段的所有子集都满足，这里有个技巧就是窗口更新后，因为和上一个窗口可能是有交集的，所以这一段的新的子数组为 right−left+1 个，自己写几个规律就出来了。

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: 'List[int]', k: int) -> int:
        if k==0 or k==1:
            return 0
        l, count = 0, 0
        total = 1
        for i in range(len(nums)):
            total*=nums[i]
            while total>=k:
                total//=nums[l]
                l+=1
            count+=i-l+1
        return count
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$



**这是当时自己写的一种，太长了，并且有些长例出错了，不知道怎么回事。**

```python
class Solution:
    def numSubarrayProductLessThanK(self, nums: 'List[int]', k: int) -> int:
        start, end = 0, 0
        count = 0
        total = nums[0]
        while end < len(nums):
            if total < k:
                count += end - start + 1
                end += 1
                total *= nums[end]
            else:
                while total >= k and start < end:
                    total //= nums[start]
                    start += 1
                if start == end and total >= k:
                    start += 1
                    end += 1
            # if start == end:
            #     start += 1
            #     end += 1
            if end == len(nums) - 1:
                while start <= end:
                    if total < k:
                        count += end - start + 1
                        return count
                    total //= nums[start]
                    start += 1
                    if start > end:
                        return count

        return count
```

