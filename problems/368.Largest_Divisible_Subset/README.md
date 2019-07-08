## 368.Largest Divisible Subset

### 题目描述

给出一个由无重复的正整数组成的集合，找出其中最大的整除子集，子集中任意一对 (Si，Sj) 都要满足：Si % Sj = 0 或 Sj % Si = 0。

如果有多个目标子集，返回其中任何一个均可。

 

**示例 1:**

```
输入: [1,2,3]
输出: [1,2] (当然, [1,3] 也正确)
```


**示例 2:**

```
输入: [1,2,4,8]
输出: [1,2,4,8]
```



### 解答

​	这道题是采用动态规划求解，dp[i]表示以i为结尾的最长的整除子集长度，pre[i]记录i前面一个数的位置，这样在最后找到最长的子集的最后一个数字后可以往前一个个找出其他的数字。但是nums要提前排序好。

```python
class Solution:
    def largestDivisibleSubset(self, nums: List[int]) -> List[int]:
        # 动态规划 dp[i]表示以i为结尾的最长的整除子集长度，pre[i]记录i前面一个数的位置
        nums.sort()
        res = []
        if len(nums)==0:
            return res
        dp = [1]*len(nums)
        pre = [-1]*len(nums)
        
        for i in range(1,len(nums)):
            for j in range(0,i):
                if nums[i]%nums[j]==0 and dp[i]<dp[j]+1:
                    dp[i] = dp[j]+1
                    pre[i] = j
        # print(dp)
        max_ix = dp.index(max(dp))
        while max_ix!=-1:
            res.append(nums[max_ix])
            max_ix = pre[max_ix]
        return res
        
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 

