## 453.Minimum Moves to Equal Array Elements

## 题目描述

给定一个长度为 n 的非空整数数组，找到让数组所有元素相等的最小移动次数。每次移动可以使 n - 1 个元素增加 1。

**示例:**

```
输入:
[1,2,3]

输出:
3

解释:
只需要3次移动（注意每次移动会增加两个元素的值）：

[1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```



### 解答

​	这道题需要换一个思路解答，n-1个数同时加一，就好比每次有一个数自身减一，最后得到的必定是最小值，这样每个元素减去最小值的和就是答案，在评论区看到一句很有意思的话，n-1个少数民族加分相当于1个民族扣分- =。

```python
class Solution(object):
    def minMoves(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # n-1个少数民族加分等于一个民族减分
        # res = 0
        # min_num = min(nums)
        # for num in nums:
        #     res+=num-min_num
        # return res
        
        # 公式法
        return sum(nums)-len(nums)*min(nums)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$