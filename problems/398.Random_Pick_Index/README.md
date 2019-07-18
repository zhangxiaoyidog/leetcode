## 398.Random Pick Index

### 题目描述

给定一个可能含有重复元素的整数数组，要求随机输出给定的数字的索引。 您可以假设给定的数字一定存在于数组中。

注意：
数组大小可能非常大。 使用太多额外空间的解决方案将不会通过测试。

**示例:**

```
int[] nums = new int[] {1,2,3,3,3};
Solution solution = new Solution(nums);

// pick(3) 应该返回索引 2,3 或者 4。每个索引的返回概率应该相等。
solution.pick(3);

// pick(1) 应该返回 0。因为只有nums[0]等于1。
solution.pick(1);
```



### 解答

​	由于数字一定存在，那么先找到第一个target出现的位置，开始遍历，如果后面还有，那么还是以蓄水池抽样算法的思想以1/count的概率选取即可。

```python
from random import randint
class Solution:
    def __init__(self, nums: List[int]):
        self.nums = nums

    def pick(self, target: int) -> int:
        # 数字一定存在
        i = 0
        while self.nums[i]!=target:
            i+=1
        # 找到第一个数字
        res = i
        count = 0
        # print(i)
        while i<len(self.nums) and self.nums[i]==target:
            # 蓄水池抽样算法
            if not randint(0, count):
                res = i
            count += 1
            i+=1
        return res
        
        
# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.pick(target)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 