## 084_Largest_Rectangle_in_Histogram

### 题目描述

给定 *n* 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 `[2,1,5,6,2,3]`。

 

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/histogram_area.png)

图中阴影部分为所能勾勒出的最大矩形面积，其面积为 `10` 个单位。

 

**示例:**

```
输入: [2,1,5,6,2,3]
输出: 10
```



### 解答1

​	这道题还是有点难度的，首先想到的肯定是暴力解决，遍历所有的可能性找出最大值，但是这样不用想肯定无法AC，提交超时，所以需要减小时间复杂度，观察发现如果`heights[i] < heights[i+1]`，我不需要遍历以`heights[i]`为最右侧所构成的所有矩形，因为以`heights[i+1]`为最右侧所构成的所有矩形肯定会大于前者，这样会节省一部分时间开销，但是还是无法AC，orz……

```python
class Solution:
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        if len(heights) == 0:
            return 0
        
        if len(heights) == 1:
            return heights[0]
        max_rectangle = heights[0]
        for i in range(len(heights)):
            if i == len(heights)-1 or heights[i]>heights[i+1]:
                for j in range(i, -1, -1):
                    max_rectangle = max(max_rectangle, min(heights[j:i+1]) * (i-j + 1))
        return max_rectangle
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)​$ 



### 解答2

​	查看DISCUSS的解答后发现一种比较巧妙的解法，就是利用单调栈，这个栈里面只存储递增或者递减的数组（即这个柱状图的下标），遍历一遍数组，假如栈空或者遇到更高的矩形，直接入栈，否则计算以此时出栈的矩形能形成的最大举行的面积，这样不断循环就可以找到最大值，详细看代码即可。

```python
class Solution:
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        if len(heights) == 0:
            return 0
        i = 0
        heights.append(0)
        max_rectangle = 0
        stack = []
        while i<len(heights):
            if len(stack) == 0 or heights[stack[-1]] <= heights[i]:
                stack.append(i)
                i+=1
            else:
                now_idx = stack.pop()
                
                if len(stack) == 0:
                    max_rectangle = max(max_rectangle,i*heights[now_idx])
                else:

                    max_rectangle = max(max_rectangle,(i-1-stack[-1])*heights[now_idx])
        return max_rectangle
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 