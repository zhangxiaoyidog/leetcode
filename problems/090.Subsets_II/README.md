## 090.Subset II

## 题目描述

给定一个可能包含重复元素的整数数组 **\*nums***，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例:**

```
输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```



### 解答

​	这道题和之前的78题是非常类似的，所以我们只需要使用我们的DFS代码模板的同时判断这个子集是否已经存在于ans数组中即可，代码还是一样的套路。这里必须要先排序，比如[4,4,4,1,4]不排序会出现[1,4]和[4,1]的情况。

```python
class Solution:
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        
        ans = []
        temp = []
        print(nums)
        self.dfs_subsets(ans,temp,nums,0)
        return ans
    
    def dfs_subsets(self,ans,temp,nums,start):
        if temp not in ans:
            ans.append(list(temp))
        for i in range(start,len(nums)):
            temp.append(nums[i])
            self.dfs_subsets(ans,temp,nums,i+1)
            temp.remove(nums[i])
```

