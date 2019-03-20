## 128.Longest Consecutive Sequence

## 题目描述

给定一个未排序的整数数组，找出最长连续序列的长度。

要求算法的时间复杂度为 *O(n)*。

**示例:**

```
输入: [100, 4, 200, 1, 3, 2]
输出: 4
解释: 最长连续序列是 [1, 2, 3, 4]。它的长度为 4。
```



### 解答

​	这道题比较难想，是属于技巧性比较强的一道题，做法是用哈希表存储每个端点值对应连续区间的长度，若是新数加入，取出其左右相邻数已有的连续区间长度 left 和 right，然后计算当前数的区间长度为：cur_length = left + right + 1，根据 cur_length 更新最大长度 max_length 的值，再更新区间两端点的长度值。

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        d = {}
        max_length = 0
        for num in nums:
            if num not in d:
                # 获取左右两个数字的连续期间长度
                left_length = d.get(num-1,0)
                right_length = d.get(num+1,0)
                
                cur_length = 1 + left_length + right_length
                if max_length<cur_length:
                    max_length = cur_length
                d[num] = cur_length
                d[num-left_length] = cur_length
                d[num+right_length] = cur_length
        return max_length
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

