## 377.Combination Sum IV

### 题目描述

给定一个由正整数组成且不存在重复数字的数组，找出和为给定目标正整数的组合的个数。

**示例:**

```
nums = [1, 2, 3]
target = 4
所有可能的组合为：
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

请注意，顺序不同的序列被视作不同的组合。
因此输出为 7。
```


**进阶：**
如果给定的数组中含有负数会怎么样？
问题会产生什么变化？
我们需要在题目中添加什么限制来允许负数的出现？



### 解答1

​	最先想到的还是采取递归回溯的方式，和[第39题](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/039.combination_sum/README.md)思路是一样的，找到所有的组合，最后返回的是list的长度，但是提交超时。

```python
class Solution(object):
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        # 回溯超时
        nums.sort()
        self.res = []
        self.dfs_search(nums,target,0,[])
        return len(self.res)
    
    def dfs_search(self,nums,target,start,values):
        if target==0:
            self.res.append(values)
        for i in range(start,len(nums)):
            if nums[i]>target:
                return
            self.dfs_search(nums,target-nums[i],start,values+[nums[i]])
```



### 解答2

​	这道题采用回溯超时，明显是要用时间复杂度更低一点的算法，那就是动态规划了，输出是长度，那么dp数组的定义肯定是和长度有关，所以定义dp[i]代表组合数为i时使用nums中的数能组成的组合数的个数，举个例子，比如题中的那个，dp[4]=dp[3]+dp[2]+dp[1]，解释起来就是，4的组合数可以由三部分组成，1和dp[3]，2和dp[2],3和dp[1];

```python
class Solution(object):
    def combinationSum4(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """

        # 动态规划
        dp = [0]*(target+1)
        dp[0] = 1
        for i in range(1,target+1):
            for num in nums:
                if i>=num:
                    dp[i] += dp[i-num]
        # print(dp)
        return dp[-1]
```

- 时间复杂度：$O(n*m)$
- 空间复杂度：$O(n)$ 