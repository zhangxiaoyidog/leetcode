## 300.Longest Increasing Subsequence

## 题目描述

给定一个无序的整数数组，找到其中最长上升子序列的长度。

**示例:**

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```

**说明:**

- 可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
- 你算法的时间复杂度应该为 O(*n2*) 。

**进阶:** 你能将算法的时间复杂度降低到 O(*n* log *n*) 吗?



### 解答

​	这道题很明显了，使用动态规划求解，由于上升子序列不一定非要是连续的，所以定义dp[i]表示以nums[i]结尾的最长上升子序列的长度，使用两个for循环遍历即可。

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        # 动态规划,不一定是连续的序列
        if len(nums)==0:
            return 0
        dp = [1]*len(nums)
        res = 1
        
        for i in range(len(nums)):
            max_val = 0
            for j in range(i):
                if nums[i]>nums[j]:
                    max_val = max(max_val,dp[j])
            dp[i] = max_val + 1
            res = max(res,dp[i])
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 



### 解答2

​	这道题题目中说可以把时间复杂度降低到O(nlogn)，也就是说中间可能会用到二分搜索，可是怎么使用二分呢，使用二分的条件就是必须要有一个有序数组，所以我们可以新建一个数组cell，用于保存最长上升子序列，遇到一个数字，就对cell进行二分搜索，插入到相应位置，如果cell中的数字都比它小，直接插到最后，否则用它替换比他大的元素中最小的那个，为什么要这样呢？因为cell中存储的是最长上升子序列，替换只是为了后面的序列的更新，并没有改变长度，所以最后必然会得到最新的最长上升子序列。

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if len(nums)<2:
            return len(nums)
        cell = [nums[0]]
        for num in nums[1:]:
            if num>cell[-1]:
                cell.append(num)
                continue
            l,r = 0,len(cell)-1
            while l<r:
                mid = l + (r - l)//2
                if cell[mid]<num:
                    l = mid + 1
                else:
                    r= mid
            cell[l] = num
        return len(cell)
```

- 时间复杂度：$O(n*logn)$
- ​空间复杂度：$O(n)$ 

