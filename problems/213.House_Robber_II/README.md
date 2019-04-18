## 213.House_Robber_II

## 题目描述

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都**围成一圈，**这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警**。

给定一个代表每个房屋存放金额的非负整数数组，计算你**在不触动警报装置的情况下，**能够偷窃到的最高金额。

**示例 1:**

```
输入: [2,3,2]
输出: 3
解释: 你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
```

**示例 2:**

```
输入: [1,2,3,1]
输出: 4
解释: 你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

### 解答

​	这道题和之前的198题是差不多的，唯一不同的是这个题目的第一个房屋和最后一个房屋是紧挨的，那么解决方式很巧妙，我们直接把它当做两个序列[0:n-1]，[1:n]去做不就好了，还是使用之前的方法，动态规划。

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        # 动态规划解题
        if len(nums) == 1:
            return nums[0]
        return max(self.rob_first(nums,0,len(nums)-1),self.rob_first(nums,1,len(nums)))
    def rob_first(self,nums,start,end):
        prev_no = 0
        prev_yes = 0
        for i in range(start,end):
            temp = prev_no
            prev_no = max(prev_no,prev_yes)
            prev_yes = nums[i]+temp
        return max(prev_no, prev_yes)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

