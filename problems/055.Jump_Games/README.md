## 055.Jump Games

### 题目描述

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个位置。

**示例 1:**

```
输入: [2,3,1,1,4]
输出: true
解释: 从位置 0 到 1 跳 1 步, 然后跳 3 步到达最后一个位置。
```

**示例 2:**

```
输入: [3,2,1,0,4]
输出: false
解释: 无论怎样，你总会到达索引为 3 的位置。但该位置的最大跳跃长度是 0 ， 所以你永远不可能到达最后一个位置。
```



### 解答１

​	首先最容易想到的当然是暴力法解题，也就是和Jump Game II的思路一样，每次去遍历当前点之前的那些点能到达的最远位置，最后如果能到达终点就返回True，如果在中途停滞不前了，直接返回False。但是这样时间复杂度比较高，提交超时orz.

```python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        cur = 0
        while cur<len(nums)-1:
            last_cur = cur
            for i in range(cur+1):
                max_temp = i+nums[i]
                cur = max(cur,max_temp)
            if cur==last_cur:
                return False
        return True
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 



### 解答2

​	细想一下解答１的做法，其实有些地方我们已经算过了，就没有必要再重复计算了，也就是每次只用计算上个最远点到目前的最远点之前的这些点能到达的最远位置就可以了，其实类似与备忘录算法，提交AC。虽然时间复杂度没变，但是实际运算减少了很多。

```python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums)==0:
            return True
        cur = nums[0]
        last_max_temp = 0
        while cur<len(nums)-1:
            last_cur = cur
            for i in range(last_max_temp,cur+1):
                max_temp = i+nums[i]
                cur = max(cur,max_temp)
            last_max_temp = last_cur
            if cur==last_cur:
                return False
        return True
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$ 



### 解答3

​	想想看既然能用备忘录算法，那么肯定是可以用动态规划的，只是需要思考这个状态转移方程如何让定义，根据以往的经验，我们可以想到把dp[i]定义为第i个位置能到达的最远的位置，可以得到dp[i] = max(dp[i-1],i+nums[i])，这样一来就可以直接看代码啦。

```python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        if len(nums)==0:
            return True
        dp = [0 for i in range(len(nums))]
        
        dp[0] = nums[0]
        for i in range(1,len(nums)):
            if dp[i-1]>=i:
                dp[i] = max(dp[i-1],i+nums[i])
            else:
                dp[i] = 0
        if dp[len(nums)-1]>=len(nums)-1:
            return True
        return False
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

### 解答4

​	解答4时使用贪心算法来解题，因为对这一块我还没有一个很好的总结和认识，所以这个解法也是借鉴了别人的一个思路，在动态规划的转移方程中，一般会比较每一种可能路径的值，再从中取最优，所以这个转移的过程进一步优化一般就是贪心算法的本质所在，贪心算法一般是通过观察问题的主要矛盾，直接从多种路径中得到最优值。代码比较易懂，这里不再过多赘述，重要的是理解和思想。

```python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        last_cur = len(nums)-1
        for i in range(len(nums)-1,-1,-1):
            if i+nums[i]>=last_cur:
                last_cur = i
        
        return last_cur==0
```



- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



