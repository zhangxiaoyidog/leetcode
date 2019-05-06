## 229.Majority Element II

## 题目描述

给定一个大小为 *n* 的数组，找出其中所有出现超过 `⌊ n/3 ⌋` 次的元素。

**说明:** 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

**示例 1:**

```
输入: [3,2,3]
输出: [3]
```

**示例 2:**

```
输入: [1,1,1,3,3,2,2,2]
输出: [1,2]
```



### 解答

​	这道题要求不能使用额外空间，结合之前求众数的那道题，还是使用摩尔投票法，该算法用于1/2情况的时候，它说：“在任何数组中，出现次数大于该数组长度一半的值只能有一个。”，那么在一个大小为n的数组中，其中超过n//3次的元素肯定不超过2个.找出次数最多的两个数，然后判断各自出现次数即可。

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> List[int]:
        # 一个大小为n的数组，其中超过n//3次的元素肯定不超过2个.找出次数最多的两个数 2.判断各自出现次数
        x = 0
        y = 0
        cx = 0
        cy = 0
        
        for num in nums:
            if (cx==0 or num==x) and num!=y:
                cx += 1
                x = num
            elif cy==0 or num==y:
                cy += 1
                y = num
            else:
                cx -= 1
                cy -= 1
        
        cx = 0
        cy = 0
        for num in nums:
            if num==x:
                cx+=1
            if num ==y:
                cy+=1
        res = []
        if cx>len(nums)//3:
            res.append(x)
        if cy>len(nums)//3:
            res.append(y) 
            
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 