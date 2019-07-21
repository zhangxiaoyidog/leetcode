## 414.Third Maximum Number

### 题目描述

给定一个非空数组，返回此数组中第三大的数。如果不存在，则返回数组中最大的数。要求算法时间复杂度必须是O(n)。

**示例 1:**

```
输入: [3, 2, 1]

输出: 1

解释: 第三大的数是 1.
```

**示例 2:**

```
输入: [1, 2]

输出: 2

解释: 第三大的数不存在, 所以返回最大的数 2 .
```

**示例 3:**

```
输入: [2, 2, 3, 1]

输出: 1

解释: 注意，要求返回第三大的数，是指第三大且唯一出现的数。

存在两个值为2的数，它们都排第二。
```



### 解答

​	使用三个变量，分别存储第一大、第二大和第三大的数字，先比较最大的，成功就把值向后传递，把第后面的丢掉，最后返回正确答案。

```python
class Solution:
    def thirdMax(self, nums: List[int]) -> int:
        if len(nums)<3:
            return max(nums)
        max1, max2, max3 = float('-inf'),float('-inf'),float('-inf')
        
        for num in nums:
            if num>max1:
                max3 = max2
                max2 = max1
                max1 = num
                continue
            
            if num!=max1 and num>max2:
                max3 = max2
                max2 = num
                continue
            
            if num!=max1 and num!=max2 and num>max3:
                max3 = num
        if max1!=float('-inf') and max2!=float('-inf') and max3!=float('-inf'):
            return max3
        return max1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$