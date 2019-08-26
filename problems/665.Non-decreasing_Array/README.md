## 665.Non-decreasing Array

## 题目描述

给定一个长度为 n 的整数数组，你的任务是判断在最多改变 1 个元素的情况下，该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的： 对于数组中所有的 i (1 <= i < n)，满足 array[i] <= array[i + 1]。

**示例 1:**

```
输入: [4,2,3]
输出: True
解释: 你可以通过把第一个4变成1来使得它成为一个非递减数列。
```

**示例 2:**

```
输入: [4,2,1]
输出: False
解释: 你不能在只改变一个元素的情况下将其变为非递减数列。
```


说明:  n 的范围为 [1, 10,000]。



### 解答

![](https://note.youdao.com/yws/api/personal/file/WEBabfaaf381f0abbdc588c8bd4438637f9?method=download&shareKey=dee076aef8d7cd37a1256ba672e80a20)

```python
class Solution:
    def checkPossibility(self, nums: List[int]) -> bool:
        if len(nums)<2:
            return True
        for i in range(len(nums)-1):
            if nums[i]>nums[i+1]:
                if i-1>=0 and nums[i-1]>nums[i+1]:
                    nums[i+1] = nums[i]
                else:
                    nums[i] = nums[i+1]
                break
        for i in range(len(nums)-1):
            if nums[i]>nums[i+1]:
                return False
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$