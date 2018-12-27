## 075.Sort Colors

### 题目描述

给定一个包含红色、白色和蓝色，一共 *n* 个元素的数组，**原地**对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

**注意:**
不能使用代码库中的排序函数来解决这道题。

**示例:**

```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```



### 解答

​	这道题的解法有几种，比较直观的解决方案是使用基数排序的两趟扫描算法，首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。但是这样需要使用额外的存储空间，所以需要采用更好的解决方案，由于本题的颜色比较少，我们可以直接统计三种元素的个数，然后顺序修改原数组的值就行了。

```python
class Solution:
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        red = 0
        white = 0
        blue = 0
        
        for num in nums:
            if num == 0:
                red+=1
            elif num == 1:
                white+=1
            else:
                blue+=1
        i = 0
        while red!=0:
            nums[i] = 0
            i+=1
            red-=1
        while white!=0:
            nums[i] = 1
            i+=1
            white-=1
        while blue!=0:
            nums[i] = 2
            i+=1
            blue-=1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 