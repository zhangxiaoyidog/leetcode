## 219.Contains Duplicate II

## 题目描述

给定一个整数数组和一个整数 *k*，判断数组中是否存在两个不同的索引 *i* 和 *j*，使得 **nums [i] = nums [j]**，并且 *i* 和 *j* 的差的绝对值最大为 *k*。

**示例 1:**

```
输入: nums = [1,2,3,1], k = 3
输出: true
```

**示例 2:**

```
输入: nums = [1,0,1,1], k = 1
输出: true
```

**示例 3:**

```
输入: nums = [1,2,3,1,2,3], k = 2
输出: false
```

### 解答

​	这个可以利用字典来解题，遍历数组的同时把数字和它的index加入到字典中，假如已经存在，那么判断和之前那个相同的数字的index差的绝对值是否小于k，如果是则返回True，否则返回False。

```python
class Solution:
    def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        index_dic = {}
        
        for i in range(len(nums)):
            if nums[i] not in index_dic:
                index_dic[nums[i]] = i
            else:
                if i - index_dic[nums[i]] <= k:
                    return True
                else:
                    index_dic[nums[i]] = i
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 