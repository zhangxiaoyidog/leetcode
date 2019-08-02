## 442.Find All Duplicates in an Array

## 题目描述

给定一个整数数组 a，其中1 ≤ a[i] ≤ n （n为数组长度）, 其中有些元素出现两次而其他元素出现一次。

找到所有出现两次的元素。

你可以不用到任何额外空间并在O(n)时间复杂度内解决这个问题吗？

**示例：**

```
输入:
[4,3,2,7,8,2,3,1]

输出:
[2,3]
```



### 解答

​	由于数组元素的大小在1和n之间，所以遍历输入数组过程中，给对应位置的数字取相反数，如果已经是负数，说明前面已经出现过，直接放入输出数组。

```python
class Solution:
    def findDuplicates(self, nums: List[int]) -> List[int]:
        res = []
        
        for i in range(len(nums)):
            temp = abs(nums[i])
            if nums[temp-1]>0:
                nums[temp-1] *= -1
            else:
                res.append(temp)
        return res  
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$