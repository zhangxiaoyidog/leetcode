## 334.Increasing Triplet Subsequence

## 题目描述

给定一个未排序的数组，判断这个数组中是否存在长度为 3 的递增子序列。

数学表达式如下:

> 如果存在这样的 i, j, k,  且满足 0 ≤ i < j < k ≤ n-1，
> 使得 arr[i] < arr[j] < arr[k] ，返回 true ; 否则返回 false 。

**说明: **要求算法的时间复杂度为 O(n)，空间复杂度为 O(1) 。

**示例 1:**

```
输入: [1,2,3,4,5]
输出: true
```

**示例 2:**

```
输入: [5,4,3,2,1]
输出: false
```

### 解答

​	这道题一开始我是想找到list中的最大值和最小值的位置，然后看中间有没有num，但是这样有一些特殊情况无法兼顾，比如1111111的这种和15235。所以还是参考了disscuss中的方案，a 始终记录最小元素，b 为某个子序列里第二大的数。接下来不断更新 a，同时保持 b 尽可能的小。如果下一个元素比 b 大，说明找到了三元组。

```python
import sys
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        if len(nums)<=3:
            return False
        a = sys.maxsize
        b = sys.maxsize
        for num in nums:
            if num <=a:
                a = num
            elif num<=b:
                b = num
            else:
                return True
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 