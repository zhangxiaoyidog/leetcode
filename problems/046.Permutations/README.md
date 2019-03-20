## 046.Permutations

### 题目描述

给定一个**没有重复**数字的序列，返回其所有可能的全排列。

**示例:**

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### 解答

这道题我是采用回溯算法来解决问题，也就是穷举所有的组合，代码很简单。

```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        if len(nums)==0:
            return []
        if len(nums)==1:
            return [nums]
        res = []
        for i in range(len(nums)):
            for j in self.permute(nums[:i]+nums[i+1:]):
                res.append([nums[i]]+j)
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 

