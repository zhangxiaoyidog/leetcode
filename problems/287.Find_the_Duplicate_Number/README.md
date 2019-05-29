## 287.Find the Duplicate Number

## 题目描述

给定一个包含 *n* + 1 个整数的数组 *nums*，其数字都在 1 到 *n* 之间（包括 1 和 *n*），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

**示例 1:**

```
输入: [1,3,4,2,2]
输出: 2
```

**示例 2:**

```
输入: [3,1,3,4,2]
输出: 3
```

**说明：**

1. **不能**更改原数组（假设数组是只读的）。
2. 只能使用额外的 *O*(1) 的空间。
3. 时间复杂度小于 *O*(*n*2) 。
4. 数组中只有一个重复的数字，但它可能不止重复出现一次。



### 解答1

​	这个问题比较容易相处的解法就实现把列表排序，然后从头到尾遍历，判断当前元素与后面一个元素是否相等，成立直接返回即可。

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        nums.sort()
        for i in range(len(nums)-1):
            if nums[i]==nums[i+1]:
                return nums[i]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	这道题还有一个比较巧妙的解法，也就是假如使用`t=nums[t]`这样的前进方式，会有如下结果。

```
t=nums[0]=1
t=nums[1]=3
t=nums[3]=2
t=nums[2]=4
t=nums[4]=2
t=nums[2]=4
...
```

也就是说必然会有环存在，再使用`t=nums[nums[t]]`这样的前进策略，结果如下。

```
t=nums[nums[0]]=3
t=nums[nums[3]]=4
t=nums[nums[4]]=4
...
```

这样的话就可以使用和142题一样的方法，快慢指针找到环的入口！

```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        # 快慢指针求解
        if len(nums)>1:
            slow = nums[0]
            fast = nums[nums[0]]
            # 先找到相遇处
            while slow!=fast:
                slow = nums[slow]
                fast = nums[nums[fast]]
            start = 0
            while start!=slow:
                start = nums[start]
                slow = nums[slow]
            return start            
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 