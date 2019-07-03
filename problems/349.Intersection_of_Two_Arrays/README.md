## 349.Intersection of Two Arrays

## 题目描述

给定两个数组，编写一个函数来计算它们的交集。

**示例 1:**

```
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2]
```

**示例 2:**

```
输入: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出: [9,4]
```

**说明:**

+ 输出结果中的每个元素一定是唯一的。
+ 我们可以不考虑输出结果的顺序。



### 解答

​	遍历一个list，判断当前数字是否在另一个list中，注意处理重复数字，另一种是直接变set取交集。

```python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        # res = []
        # if len(nums1)==0 or len(nums2)==0:
        #     return res
        # for num in nums1:
        #     if num in nums2 and num not in res:
        #         res.append(num)
        # return res
        
        return list(set(nums1)&set(nums2))
```

