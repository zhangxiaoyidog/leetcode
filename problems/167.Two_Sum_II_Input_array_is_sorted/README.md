## 167.Two Sum II - Input array is sorted

## 题目描述

给定一个已按照**升序排列** 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2*。*

**说明:**

- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

**示例:**

```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```



### 解答

​	这道题和第一道题很相似，不过这道题是有序数组，所以我们可以用双指针法，如果当前的和小于target，那么l指针往后走，大于则r指针往前走。否则等于直接return。

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        # 由于升序，那就使用双指针
        l = 0
        r = len(numbers) - 1
        while l<=r:
            sums = numbers[l] + numbers[r]
            if sums == target:
                return [l+1,r+1]
            elif sums < target:
                l += 1
            else:
                r-=1
        # print(l,r)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$