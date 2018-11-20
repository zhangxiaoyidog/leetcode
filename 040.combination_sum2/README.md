## 040.**Combination Sum 2**

### 题目描述

给定一个数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用一次。

**说明：**

- 所有数字（包括目标数）都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```

### 解答

​	这道题思路和前面的那道题一样，都是采用DFS求解，只是这里每个数字在每个组合只能使用一次要注意一下。

```python
class Solution:
    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()
        self.result = []
        self.search(candidates,target,0,[])
        return self.result
    def search(self,candidates,target,start,values):
        if target == 0 and values not in self.result:  
            return self.result.append(values)
        for i in range(start,len(candidates)):
            if candidates[i]>target:
                return
            self.search(candidates,target-candidates[i],i+1,values+[candidates[i]])
```

- 时间复杂度：？
- 空间复杂度：$O(n)$

