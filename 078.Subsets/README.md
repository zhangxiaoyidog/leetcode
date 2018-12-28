## 078.Subsets

### 题目描述

给定一组**不含重复元素**的整数数组 *nums*，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例:**

```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```



### 解答

​	这道题其实跟上一道题有一定的相似之处，可以使用我们的递归算法进行求解，即对给定的数字进行深度优先搜索(DFS)，在做递归的时候，要在适当的时机回溯，并且在递归调用的时候，需要传递的参数都是什么，状态传递，递归出口这些一定要注意好，其实这一类问题都可以用以下的代码框架去解决，但是在求排列的时候需要考虑是否已有，和46题类似。

```python
class Solution:
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        # 使用dfs求解
        nums.sort()
        ans = []
        temp = []
        self.dfs_subsets(ans,temp,nums,0)
        return ans
    
    def dfs_subsets(self,ans,temp,nums,start):
        ans.append(list(temp)) #　一般会根据问题的不一样在这一步修改
        for i in range(start,len(nums)):
            #　一般会根据问题的不一样在这一步加一些判断条件
            temp.append(nums[i])
            self.dfs_subsets(ans,temp,nums,i+1)
            temp.remove(nums[i])
```

