## 376.Wiggle Subsequence

### 题目描述

如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为摆动序列。第一个差（如果存在的话）可能是正数或负数。少于两个元素的序列也是摆动序列。

例如， [1,7,4,9,2,5] 是一个摆动序列，因为差值 (6,-3,5,-7,3) 是正负交替出现的。相反, [1,4,7,2,5] 和 [1,7,4,5,5] 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。

给定一个整数序列，返回作为摆动序列的最长子序列的长度。 通过从原始序列中删除一些（也可以不删除）元素来获得子序列，剩下的元素保持其原始顺序。

**示例 1:**

```
输入: [1,7,4,9,2,5]
输出: 6 
解释: 整个序列均为摆动序列。
```

**示例 2:**

```
输入: [1,17,5,10,13,15,10,5,16,8]
输出: 7
解释: 这个序列包含几个长度为 7 摆动序列，其中一个可为[1,17,10,13,10,16,8]。
```

**示例 3:**

```
输入: [1,2,3,4,5,6,7,8,9]
输出: 2
```

**进阶:**
你能否用 O(n) 时间复杂度完成此题?



### 解答1

​	采用交替标记的方法，维护两个变量up和dowm，在循环中分别表示在位置i时是上升和下降两种情况时的最长摆动序列的长度，假如在位置i的数字比i-1位置大，则更新up的值为dowm+1，若小于，那么此时可以更新down的值为up+1。

```
class Solution(object):
    def wiggleMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 交替标记
        if len(nums)<2:
            return len(nums)
        down = 1
        up = 1
        for i in range(1,len(nums)):
            if nums[i-1]<nums[i]:
                up = down+1
            if nums[i-1]>nums[i]:
                down = up+1
        return max(down,up)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	使用动态规划的思想，定义down和up两个list，分别表示在位置i时是上升和下降两种情况时的最长摆动序列的长度。其实后面想了一下是可以照着上面的思想优化的。

```python
class Solution(object):
    def wiggleMaxLength(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """ 
        # 动态规划
        if len(nums)<2:
            return len(nums)
        down = [1]*len(nums)
        up = [1]*len(nums)

        for i in range(1,len(nums)):
            for j in range(i):
                if nums[i]>nums[j]:
                    up[i] = max(up[i],down[j]+1)
                if nums[i]<nums[j]:
                    down[i] = max(down[i],up[j]+1)
        # print(up,down)
        return max(up[-1],down[-1])
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 