## 179.Largest Number

## 题目描述

给定一组非负整数，重新排列它们的顺序使之组成一个最大的整数。

**示例 1:**

```
输入: [10,2]
输出: 210
```

**示例 2:**

```
输入: [3,30,34,5,9]
输出: 9534330
```

**说明:** 输出结果可能非常大，所以你需要返回一个字符串而不是整数。



### 解答

​	这道题先把所有的数字转化成字符串，然后用一个sorted函数排序后把第一位最大的数字放在最前面，然后直接join返回，这里有一种情况要注意，如果只使用sorted函数，那么30会在3前面，那这样就是错误的，因为330>303，所以要在key里面定义一个比较函数。

```python

class LargerNumKey(str):
    def __lt__(x, y):
        return x + y > y + x


class Solution:
    def largestNumber(self, nums):
        largest_num = ''.join(sorted(map(str, nums), key=LargerNumKey))
        return '0' if largest_num[0] == '0' else largest_num
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$

