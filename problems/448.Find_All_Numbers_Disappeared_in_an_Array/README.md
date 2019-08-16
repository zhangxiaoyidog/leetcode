## 448.Find All Numbers Disappeared in an Array

## 题目描述

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

**示例:**

```
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```



### 解答

​	这道题的解法和[442](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/442.Find_All_Duplicates_in_an_Array/README.md)的解法十分相似，将所有的正数作为下标，置对应的数组值为负值，那么最后仍然为正数的位置即为没出现过的数字。

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        """
        [4,3,2,7,8,2,3,1]
        [-4,-3,-2,-7,8,2,-3,-1]
        """
        res = []
        for num in nums:
            temp = abs(num)
            if nums[temp-1]>0:
                nums[temp-1] *= -1
        for i in range(len(nums)):
            if nums[i]>0:
                res.append(i+1)
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

