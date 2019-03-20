## 042.Trapping Rain Water

### 题目描述

给定 *n* 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rainwatertrap.png)

上面是由数组 [0,1,0,2,1,0,1,3,2,1,2,1] 表示的高度图，在这种情况下，可以接 6 个单位的雨水（蓝色部分表示雨水）。 **感谢 Marcos** 贡献此图。

**示例:**

```
输入: [0,1,0,2,1,0,1,3,2,1,2,1]
输出: 6
```

### 解答

​	这道题我是采用了先找到一个最高的峰，然后分别计算两边的雨水量的方法，以左边为例，从0开始遍历，初始化一个指针，若此时比指针所指位置高，则指针移位，否则计算雨量，这个做法巧妙在于找到了最大木板的index,于是在我们向这块最大木板逼近时，我们不用担心右边界或者左边界过低的问题。只用记录移动中的高峰，然后不断更新我们的面积即可。

```python
class Solution:
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        if len(height)==0:
            return 0
        hold = 0
        first = 0
        tallest = height.index(max(height))
        
        for i in range(tallest):
            if first<height[i]:
                first=height[i]
            else:
                hold+=first-height[i]
        j = len(height)-1
        first = 0
        while j>tallest:
            if first<height[j]:
                first=height[j]
            else:
                hold+=first-height[j]
            j-=1
        return hold
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 