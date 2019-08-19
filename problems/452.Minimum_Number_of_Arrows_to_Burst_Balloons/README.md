## 452.Minimum Number of Arrows to Burst Balloons

## 题目描述

在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以y坐标并不重要，因此只要知道开始和结束的x坐标就足够了。开始坐标总是小于结束坐标。平面内最多存在104个气球。

一支弓箭可以沿着x轴从不同点完全垂直地射出。在坐标x处射出一支箭，若有一个气球的直径的开始和结束坐标为 xstart，xend， 且满足  xstart ≤ x ≤ xend，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。

**Example:**

```
输入:
[[10,16], [2,8], [1,6], [7,12]]

输出:
2

解释:
对于该样例，我们可以在x = 6（射爆[2,8],[1,6]两个气球）和 x = 11（射爆另外两个气球）。
```



### 解答1

​	常规思路就是按照左边界排序后往前遍历，每次找出有重叠公共区间的气球，这些可以用一个弓箭来射爆，遍历的过程中调整l和r。

```python
class Solution(object):
    def findMinArrowShots(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        # 常规思路
        if len(points)<2:
            return len(points)
        
        res = 1
        points.sort()
        # print(points)
        l = points[0][0]
        r = points[0][1]

        for i in range(1, len(points)):
            if points[i][0]<=r:
                l = max(l, points[i][0])
                r = min(r, points[i][1])
            else:
                l = points[i][0]
                r = points[i][1]
                res+=1
        return res
```

- 时间复杂度：$O(nlogn)$
- 空间复杂度：$O(1)$



### 解答2

​	自己看一些这道题，是不是和区间调度非常相似，是的！我们可以用贪心算法来做，先根据右边界排序，设置一个 `end` 标记， 它表示：**在遍历的过程中使用当前这只箭能够击穿所有气球的最远距离**。这个最远距离，在遇到一个左边界大于它的气球时就会更新。其实上面的思路上也是贪心的思想，只不过代码比较繁琐。

```python
class Solution(object):
    def findMinArrowShots(self, points):
        """
        :type points: List[List[int]]
        :rtype: int
        """
        #贪心
        if len(points)<2:
            return len(points)
        points = sorted(points,key=lambda x:x[1])
        res = 1
        last = points[0][1]
        for i in range(1, len(points)):
            if last < points[i][0]:
                res+=1
                last = points[i][1]
        return res
```

- 时间复杂度：$O(nlogn)$
- 空间复杂度：$O(1)$