## 045.Jump Game II

### 题目描述

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

**示例:**

```
输入: [2,3,1,1,4]
输出: 2
解释: 跳到最后一个位置的最小跳跃数是 2。
     从下标为 0 跳到下标为 1 的位置，跳 1 步，然后跳 3 步到达数组的最后一个位置。
```

**说明:**

假设你总是可以到达数组的最后一个位置。

### 解答

​	首先这道题需要一个逆向思维，通常在解这个题的时候总会思考从当前点a和从a最多能跳到b的这段距离上的点最多能跳多远，但是这样会有一个数组越界问题，因此得换一种思路，也就是去遍历当前点前面的这些点最多能跳多远，然后跳到这一点，然后再判断要不要继续循环。

```python
class Solution:
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        jump = 0
        cur = 0
        i = 0
        while cur < len(nums) - 1:
            cur_temp = cur
            while i<=cur_temp:
                cur = max(i + nums[i], cur)
                i+=1
            jump+=1
        return jump
            
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$