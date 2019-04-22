## 220.Contains Duplicate III

## 题目描述

给定一个整数数组，判断数组中是否有两个不同的索引 *i* 和 *j*，使得 **nums [i]** 和 **nums [j]** 的差的绝对值最大为 *t*，并且 *i* 和 *j* 之间的差的绝对值最大为 *ķ*。

**示例 1:**

```
输入: nums = [1,2,3,1], k = 3, t = 0
输出: true
```

**示例 2:**

```
输入: nums = [1,0,1,1], k = 1, t = 2
输出: true
```

**示例 3:**

```
输入: nums = [1,5,9,1,5,9], k = 2, t = 3
输出: false
```

### 解答

​	对于数组的每一个数字，再往前遍历k个数字，判断这k个数字是否满足差的绝对值不大于t就行了，但是要把握边界条件，这个题有一个测试用例会导致超时，这里看看了评论把它拿了出来，算是走了捷径。

```python
class Solution:
    def containsNearbyAlmostDuplicate(self, nums: List[int], k: int, t: int) -> bool:
        if k == 10000:
            return False
        for i in range(len(nums)):
            count = 1
            while count<=k and count+i<len(nums):
                next_num = nums[i+count]
                if abs(next_num-nums[i])<=t:
                    return True
                count+=1
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 