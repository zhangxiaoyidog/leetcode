## 136.Single Number

## 题目描述

给定一个**非空**整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

**说明：**

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

**示例 1:**

```
输入: [2,2,1]
输出: 1
```

**示例 2:**

```
输入: [4,1,2,1,2]
输出: 4
```



### 解答1

​	第一种就是暴力搜索，遍历的同时判断这个数字是否在除了这个数字的剩下的列表中，不是即返回。

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:

        for i in range(len(nums)):
            if nums[i] not in nums[:i]+nums[i+1:]:
                return nums[i]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$  



### 解答2

​	第二种解法的技巧性比较高，需要使用逻辑位运算，想一下出现两次的元素都消去就好了，那就可以使用异或运算，不同则是1，最后剩下的肯定是那个只出现一次的。

​	其实还有一种解法是使用字典存储，这个在下一道题会使用。

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        # 一个数字和自己异或一次会变成0。
        res = 0
        for i in range(len(nums)):
            res ^= nums[i]
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$  

