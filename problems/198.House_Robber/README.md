## 198.House Robber

## 题目描述

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警**。

给定一个代表每个房屋存放金额的非负整数数组，计算你**在不触动警报装置的情况下，**能够偷窃到的最高金额。

**示例 1:**

```
输入: [1,2,3,1]
输出: 4
解释: 偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 2:**

```
输入: [2,7,9,3,1]
输出: 12
解释: 偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 
```



### 解答1

​	这道题可以使用递归来求解，假如在此房子偷（idx），那么剩下的房子为nums[idx+2:]，如果不偷剩下的为nums[idx+1:]，把握好边界条件递归就行了。但是提交超时，仔细分析一下有很多地方是重复运算了，可以改进。

```python
class Solution:
    def rob(self, nums: List[int]) -> int:

        return self.rob_id(0,nums)

        
    def rob_id(self,idx,nums):
        # 分为偷和不偷两种情况
        if idx>len(nums)-1:
            return 0
        yes = nums[idx] + self.rob_id(idx+2,nums)
        no = 0+self.rob_id(idx+1,nums)
        return max(yes,no)
```

### 解答2

​	改进第一种算法就是使用备忘录算法，看下面这张图就知道了。

![](https://note.youdao.com/yws/api/personal/file/WEBb52973f52a4977bedc09c59a14306f75?method=download&shareKey=4aaca3587e1f91396dd6194463888b2b)

​	

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        
        dic = {}
        return self.rob_id(0,nums,dic)

        
    def rob_id(self,idx,nums,dic):
        # 分为偷和不偷两种情况
        if idx>len(nums)-1:
            return 0
        if idx in dic:
            return dic[idx]
        yes = nums[idx] + self.rob_id(idx+2,nums,dic)
        no = 0+self.rob_id(idx+1,nums,dic)
        dic[idx] = max(yes,no)
        return max(yes,no)
```



### 解答3

​	第三种就是使用动态规划了，其实一开始我就在思考能不能用动态规划来做，但是这个不同于之前常规的动态规划，这里需要的定义两个状态，也就是说一个二位的列表，dp\[i][0]表示第i个屋不偷获得的最大现金，dp\[i][0]表示第i个屋偷获得的最大现金。

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) == 0:
            return 0
        # dp[i][0]表示第i个屋不偷获得的最大现金 dp[i][0]表示第i个屋偷获得的最大现金
        dp = [[0]*len(nums) for i in range(2)]
        # print(dp)
        dp[1][0] = nums[0]
        for i in range(1,len(nums)):
            dp[0][i] = max(dp[0][i-1],dp[1][i-1])
            dp[1][i] = nums[i] + dp[0][i-1]
        # print(dp)
        return max(dp[0][len(nums)-1],dp[1][len(nums)-1])
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 