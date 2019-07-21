## 410.Split Array Largest Sum

### 题目描述

给定一个非负整数数组和一个整数 m，你需要将这个数组分成 m 个非空的连续子数组。设计一个算法使得这 m 个子数组各自和的最大值最小。

**注意:**
数组长度 n 满足以下条件:

+ 1 ≤ n ≤ 1000
+ 1 ≤ m ≤ min(50, n)

**示例:**

```
输入:
nums = [7,2,5,10,8]
m = 2

输出:
18

解释:
一共有四种方法将nums分割为2个子数组。
其中最好的方式是将其分为[7,2,5] 和 [10,8]，
因为此时这两个子数组各自的和的最大值为18，在所有情况中最小。
```



### 解答1

​	第一种就是暴力递归，我们可以用深度优先搜索去生成所有的分割方案。对于数组中的每个元素，我们可以把它附加到之前的子数组上或者以这个数开始一个新的子数组（如果数组的长度不超过 m）。同时更新每个子数组的和。

```python
class Solution:
    def splitArray(self, nums: List[int], m: int) -> int:
        self.res = float('inf')
        self.m = m
        self.dfs(0,nums,0,0,0)
        return self.res
    def dfs(self,i,nums,curSub,curMax,curSum):
        if i==len(nums) and curSub==self.m:
            self.res = min(self.res,curMax)
            return
        if i==len(nums):
            return
        # 加到之前的数组中
        if i>0:
            self.dfs(i+1,nums,curSub,max(curMax,curSum+nums[i]),curSum+nums[i])

        # 新开一个数组
        if curSub<self.m:
            self.dfs(i+1,nums,curSub+1,max(curMax,nums[i]),nums[i])       
```



### 解答2

​	使用动态规划，dp\[i][j]表示将 nums[0..i]分成 j 份时能得到的最小的分割子数组最大值，后面的分割不会影响到前面分割确定的值，对于第 j 个子数组，它为数组中下标 k + 1 到 i 的这一段。因此，f\[i][j] 可以从 max(f\[k][j - 1], nums[k + 1] + ... + nums[i]) 这个公式中得到。遍历所有可能的 k，会得到 f\[i][j] 的最小值。
	但是提交超时，需要优化，比较麻烦，可以请读者自己尝试一下。

```python
class Solution:
    def splitArray(self, nums: List[int], m: int) -> int:
        # 动态规划
        sub = [0]*(len(nums)+1)
        dp = [[float('inf')]*(m+1) for _ in range(len(nums)+1)]
        for i in range(len(nums)):
            sub[i+1] = sub[i]+nums[i]
        # print(sub)
        dp[0][0] = 0
        for i in range(1,len(nums)+1):
            for j in range(1,m+1):
                for k in range(i):
                    dp[i][j] = min(dp[i][j],max(dp[k][j-1], sub[i]-sub[k]))
        
        # print(dp)
        return dp[i][j]
```

- 时间复杂度：$O(n^3)$
- 空间复杂度：$O(n^3)$



### 解答3

​	二分法真的是个好方法，将数组分成m个非空的连续子数组，求出这 m 个子数组各自和的最大值最小。这个最小的最大值肯定在max(nums)和sum(nums)中的一个，那么可以用二分法来找到这个值，如果我们找到了一种分割方案，使得最大的分割子数组和不超过 mid，那么我们也能找到一种分割方案使得最大的分割子数组和不超过 y，其中 y大于x。对于值 x，我们把这个性质定义为 `F(x)`，对于mid，如果F(mid)为真，那么说明可以找到一种分割，使得最大为mid，那么需要往下找，也就是end=mid-1。

```python
class Solution:
    def splitArray(self, nums: List[int], m: int) -> int:
        def valid(nums,target,m):
            count = 1
            total = 0
            for num in nums:
                total+=num
                if total>target:
                    count+=1
                    total=num
                    if count>m:
                        return False
            return True
        start,end = max(nums),sum(nums)
        while start<=end:
            mid = start + (end-start)//2
            if valid(nums,mid,m):
                
                end = mid-1
            else:
                start = mid+1
        return start
```

- 时间复杂度：$O(nlogm)$
- 空间复杂度：$O(1)$