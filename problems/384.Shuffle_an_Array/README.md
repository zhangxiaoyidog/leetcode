## 384.Shuffle an Array

### 题目描述

打乱一个没有重复元素的数组。

示例:

```
// 以数字集合 1, 2 和 3 初始化数组。
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// 打乱数组 [1,2,3] 并返回结果。任何 [1,2,3]的排列返回的概率应该相同。
solution.shuffle();

// 重设数组到它的初始状态[1,2,3]。
solution.reset();

// 随机返回数组[1,2,3]打乱后的结果。
solution.shuffle();
```



### 解答

```python
class Solution:

    def __init__(self, nums: List[int]):
        self.array = nums
        self.original = list(nums)

    def reset(self) -> List[int]:
        """
        Resets the array to its original configuration and return it.
        """
        self.array = self.original
        self.original = list(self.original)
        return self.original
    def shuffle(self) -> List[int]:
        """
        Returns a random shuffling of the array.
        """
        temp = []
        n = len(self.array)
        for i in range(n):
            r = random.randint(0,n-i-1)
            temp.append(self.array.pop(r))
        self.array = list(temp)
        return self.array
        


# Your Solution object will be instantiated and called as such:
# obj = Solution(nums)
# param_1 = obj.reset()
# param_2 = obj.shuffle()
```

