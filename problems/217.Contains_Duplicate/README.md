## 217.Contains Duplicate

## 题目描述

给定一个整数数组，判断是否存在重复元素。

如果任何值在数组中出现至少两次，函数返回 true。如果数组中每个元素都不相同，则返回 false。

**示例 1:**

```
输入: [1,2,3,1]
输出: true
```

**示例 2:**

```
输入: [1,2,3,4]
输出: false
```

**示例 3:**

```
输入: [1,1,1,3,3,4,3,2,4,2]
输出: true
```



### 解答

​	这道题利用set的特性可以很简单解题。

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        set1 = set(nums)
        if len(set1) == len(nums):
            return False
        else:
            return True
```

- 时间复杂度：$O(1)$
- 空间复杂度：$O(n)$ 