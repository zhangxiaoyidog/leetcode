## 416.Partition Equal Subset Sum

## 题目描述

给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**注意:**

1. 每个数组中的元素不会超过 100
2. 数组的大小不会超过 200

**示例 1:**

```
输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
```



**示例 2:**

```
输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.
```



### 解答1

​	一开始想到的是用之前求子集的回溯方法，找到和为sum(nums)//2的子集，但是很遗憾，提交超时。还想到先排序然后直接分割成两半，这肯定也是不行的。

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        def dfs(nums,first,target,start):
            if first==target:
                return True
            for i in range(start,len(nums)):
                first+=nums[i]
                if dfs(nums,first,target,i+1):
                    return True
                first-=nums[i]
        
            return False
        
        s = sum(nums)
        if s%2!=0:
            return False
        target = s // 2
        return dfs(nums,0,target,0)
```



### 解答2

​	可以把问题转化一下，分成两个子集使他们的和是相等的，和刚才一个思路就是从数组中挑出一些正整数，使得和为全部数组元素的和的一半，这里其实和0-1背包问题十分相似，那么可以定义`dp[i][j]` ：表示能否从数组的 `[0, i]` 这个子区间内挑选一些正整数，每个数只能用一次，使得这些数的和等于 `j`，加入新来一个数字num[i]，对于它可能会被选也可能不被选，如果前i-1个已经可以挑出几个数得到j，那么不选也行，或者另一种情况是前i-1个可以挑出几个数得到j-num[i]，那么我们就挑它，这样也可以得到j。提交可以AC.

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        # nums.sort()
        # for i in range(1,len(nums)):
        #     if sum(nums[:i])==sum(nums[i:]):
        #         return True
        # return False
        
        s = sum(nums)
        if s%2!=0:
            return False
        target = s // 2
        # dp[i][j]表示从nums[:i+1]中挑一些数字是否使得和为j
        dp = [[0]*(target+1) for _ in range(len(nums))]
        
        # 第一个数字能否为target
        for i in range(target+1):
            if nums[0]==i:
                dp[0][i]=1
        for i in range(1,len(nums)):
            for j in range(target+1):
                if j >= nums[i]:
                    # 前i个能找到 前i+1个必然能找到
                    dp[i][j] = dp[i - 1][j] or dp[i - 1][j - nums[i]]
                else:
                    dp[i][j] = dp[i - 1][j]
        # print(dp)
        return dp[-1][-1]==1
```



### 解答3

​	看了discuss后恍然大悟，有些状态其实不必要再算了，并且下面的状态是由上面的状态继承下来的，用个一维状态数组是不是就够了。

```python
        s = sum(nums)
        if s%2!=0:
            return False
        target = s // 2
        # 用一维度表示
        dp = [0]*(target+1)
        for i in range(target+1):
            if nums[0]==i:
                dp[i]=1
                break
        for i in range(1,len(nums)):
            # 从后往前计算，节省不必要的计算
            for j in range(target,-1,-1):
                if j >= nums[i]:
                    dp[j] = dp[j] or dp[j - nums[i]]
                else:
                    break
                    # dp[i][j] = dp[i - 1][j]
        # print(dp)
        return dp[-1]==1
    
```

