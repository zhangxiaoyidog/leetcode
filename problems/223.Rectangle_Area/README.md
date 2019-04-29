## 223.Rectangle Area

## 题目描述

在**二维**平面上计算出两个**由直线构成的**矩形重叠后形成的总面积。

每个矩形由其左下顶点和右上顶点坐标表示，如图所示。

![Rectangle Area](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/rectangle_area.png)

**示例:**

```
输入: -3, 0, 3, 4, 0, -1, 9, 2
输出: 45
```

**说明:** 假设矩形面积不会超出 **int** 的范围。



### 解答

​	这道题比较简单，首先判断是否有重合部分，没有直接返回两个矩形的面积和，否则计算出重叠面积，用面积和减去重叠面积即可。

```python
class Solution:
    def computeArea(self, A: int, B: int, C: int, D: int, E: int, F: int, G: int, H: int) -> int:
        s1 = (C-A)*(D-B)
        s2 = (G-E)*(H-F)
        
        if A>=G or C<=E or B>=H or D<=F:
            return s1+s2
        
        else:
            i1 = max(A,E)
            i2 = max(B,F)
            i3 = min(C,G)
            i4 = min(D,H)
            s3 = (i3-i1)*(i4-i2)
            return s1+s2-s3
```

- 时间复杂度：$O(1)$
- 空间复杂度：$O(1)$ 