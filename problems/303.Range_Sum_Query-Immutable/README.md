## 303.Range Sum Query - Immutable

## 题目描述

给定一个整数数组  *nums*，求出数组从索引 *i* 到 *j*  (*i* ≤ *j*) 范围内元素的总和，包含 *i,  j* 两点。

**示例：**

```
给定 nums = [-2, 0, 3, -5, 2, -1]，求和函数为 sumRange()

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

**说明:**

1. 你可以假设数组不可变。
2. 会多次调用 *sumRange* 方法。



### 解答

​	由于需要多次调用sumRange函数，所以提前存好0-n的和，在计算的数组从索引 *i* 到 *j*  (*i* ≤ *j*) 范围内元素的总和时，用0-j的和减去0-i的和再加上num[i]即可。

```python
class NumArray:

    def __init__(self, nums: List[int]):
        # 由于需要多次调用sumRange函数，所以提前存好0-n的和
        self.nums = nums
        self.num_sum = []
        temp_sums = 0
        for i,num in enumerate(nums):
            temp_sums += num
            self.num_sum.append(temp_sums)
            
        
    def sumRange(self, i: int, j: int) -> int:
        return self.num_sum[j]-self.num_sum[i]+self.nums[i]


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(i,j)
```

