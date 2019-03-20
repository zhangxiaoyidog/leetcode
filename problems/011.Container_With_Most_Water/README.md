## 011 Container With Most Water

### 题目描述

给定 *n* 个非负整数 *a*1，*a*2，...，*a*n，每个数代表坐标中的一个点 (*i*, *ai*) 。在坐标内画 *n* 条垂直线，垂直线 *i* 的两个端点分别为 (*i*, *ai*) 和 (*i*, 0)。找出其中的两条线，使得它们与 *x* 轴共同构成的容器可以容纳最多的水。

**说明：** 你不能倾斜容器，且 *n* 的值至少为 2。

![img](https://aliyun-lc-upload.oss-cn-hangzhou.aliyuncs.com/aliyun-lc-upload/uploads/2018/07/25/question_11.jpg)

图中垂直线代表输入数组 [1,8,6,2,5,4,8,3,7]。在此情况下，容器能够容纳水（表示为蓝色部分）的最大值为 49。

**示例:**

```python
输入: [1,8,6,2,5,4,8,3,7]
输出: 49
```

## 解法1

​	这样题暴力法是最直接的，相当于排列组合，不断从n个数字中选两个组合成容器，比较出装水最多的组合即可，这样的话有$\frac{n*(n-1)}{2}$种组合，最后时间复杂度也是很高的，提交后时间超时。

```python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        # 暴力解
        max_keep = 0
        for i in range(len(height)):
            for j in range(i+1,len(height)):
                max_keep = max(max_keep,(j-i) * min(height[i],height[j]))
        return max_keep
```

复杂度分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

# 解答2

​	这道题可以使用双指针法来求解，思考一下，其实两个线段之间形成的区域总是会受到其中短的那一条线段的限制。并且一般情况下，距离越长，面积会越大。所以可以在一开始使用头为两个指针，每一次只移动较短线段对应的那个指针，直到两个指针碰头为止，剩下的问题就是我们到底要移动哪个指针，如果移动指向较长线段的指针，无论移动后指向的线段比之前更长还是更短，受到另一条线段的限制，容积都会减少，相反如果移动指向较短线段的指针，是有一定几率增大容积的。

```python
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        # 双指针法
        left = 0
        right = len(height) - 1
        max_keep = 0
        while left<right:
            max_keep = max(max_keep,min(height[left],height[right])*(right-left))
            if height[left]<=height[right]:
                left+=1
            else:
                right-=1
        return max_keep
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$

