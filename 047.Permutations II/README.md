## 047.Permutations II

### 题目描述

给定一个可包含重复数字的序列，返回所有不重复的全排列。

**示例:**

```
输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

### 解答

这道题和上面的那道题其实差不多，加一个判断条件就可以了。

```python
class Solution:
    def permuteUnique(self, nums):
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
            for c in self.permuteUnique(nums[:i]+nums[i+1:]):
                if [nums[i]]+c not in res:
                    res.append([nums[i]]+c)
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 

