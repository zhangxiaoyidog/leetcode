## 135.Candy

## 题目描述

老师想给孩子们分发糖果，有 *N* 个孩子站成了一条直线，老师会根据每个孩子的表现，预先给他们评分。

你需要按照以下要求，帮助老师给这些孩子分发糖果：

- 每个孩子至少分配到 1 个糖果。
- 相邻的孩子中，评分高的孩子必须获得更多的糖果。

那么这样下来，老师至少需要准备多少颗糖果呢？

**示例 1:**

```
输入: [1,0,2]
输出: 5
解释: 你可以分别给这三个孩子分发 2、1、2 颗糖果。
```

**示例 2:**

```
输入: [1,2,2]
输出: 4
解释: 你可以分别给这三个孩子分发 1、2、1 颗糖果。
     第三个孩子只得到 1 颗糖果，这已满足上述两个条件。
```



### 解答

​	这道题不是很难，通过两遍扫描解决问题，首先每人最少分一个，第一遍扫描，确保比左边孩子表现好的比左边要多一个，第二遍扫描，确保比右边大的孩子比右边多一个。

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:
        if len(ratings) == 0:
            return 0
        # 每人最少一个
        res = [1] * len(ratings)

        # 第一遍扫描，确保比左边大的孩子比左边多一个
        for i in range(1 ,len(ratings)):
            if ratings[i] > ratings[i-1]:
                res[i] = res[i-1]+1
        # 第二遍扫描，确保比右边大的孩子比右边多一个
        for i in range(len(ratings)-2,-1,-1):
            if ratings[i] > ratings[i+1] and res[i]<=res[i+1]:
                res[i] = res[i+1]+1   
        sums = 0
        for i in range(len(res)):
            sums+=res[i]
        return sums
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 