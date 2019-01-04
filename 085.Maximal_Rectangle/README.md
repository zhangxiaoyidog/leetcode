## 085.Maximal_Rectangle

### 题目描述

给定一个仅包含 0 和 1 的二维二进制矩阵，找出只包含 1 的最大矩形，并返回其面积。

**示例:**

```
输入:
[
  ["1","0","1","0","0"],
  ["1","0","1","1","1"],
  ["1","1","1","1","1"],
  ["1","0","0","1","0"]
]
输出: 6
```

### 解答

​	这道题和前面的84题有一定的相似之处，其实可以转化为84题来求解，具体做法是一层一层去看，也就是遍历matrix中的每一行，把它转化成直方图，也就是84中的heights数组，然后把84的函数直接拿过来用就行了。

```python
class Solution:
    def maximalRectangle(self, matrix):
        """
        :type matrix: List[List[str]]
        :rtype: int
        """
        
        def largestRectangleArea(heights):
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
        if len(matrix) == 0 or len(matrix[0])==0:
            return 0
        m = len(matrix)
        
        n = len(matrix[0])
        heights = []
        # 先计算第一层
        for i in range(n):
            if matrix[0][i] == "1":
                heights.append(1)
            else:
                heights.append(0)
        print(heights)
        res = largestRectangleArea(heights)
        for i in range(1,m):
            for j in range(n):
                if matrix[i][j] == "1":
                    heights[j]+=1
                else:
                    heights[j]=0
            
            res = max(res,largestRectangleArea(heights))
        return  res
        
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 