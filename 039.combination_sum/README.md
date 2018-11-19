## 039.**Combination Sum**

### 题目描述

给定一个**无重复元素**的数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的数字可以无限制重复被选取。

**说明：**

- 所有数字（包括 `target`）都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [2,3,6,7], target = 7,
所求解集为:
[
  [7],
  [2,2,3]
]
```

**示例 2:**

```
输入: candidates = [2,3,5], target = 8,
所求解集为:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

### 解答

​	这道题一开始没有很好的思路，但是大概知道应该用回溯算法深度优先遍历这一类的递归求解，看了别人了解题思路发现使用回溯算法就可以很好的解决问题，具体细节看代码即可。

```python
class Solution:
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()
        self.re_list = []
        self.search(candidates, target, 0, [])
        return self.re_list
    #深度优先遍历
    def search(self, candidates, target, start, values):
        if target == 0:
            # 满足要求即返回
            return self.re_list.append(values)
        for i in range(start, len(candidates)):
            # candidates是有序的，这时这条路已经走到尽头
            if candidates[i] > target:
                return
            # 再向下搜索，由于有序且一个元素可以重复出现，则start赋值为i

            self.search(candidates, target - candidates[i], i, values+[candidates[i]])
```

- 时间复杂度：？
- 空间复杂度：$O(n)$