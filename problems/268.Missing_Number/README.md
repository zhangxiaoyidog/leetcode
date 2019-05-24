## 268.Missing Number

## 题目描述

给定一个包含 `0, 1, 2, ..., n` 中 *n* 个数的序列，找出 0 .. *n* 中没有出现在序列中的那个数。

**示例 1:**

```
输入: [3,0,1]
输出: 2
```

**示例 2:**

```
输入: [9,6,4,2,3,5,7,0,1]
输出: 8
```

**说明:**
你的算法应具有线性时间复杂度。你能否仅使用额外常数空间来实现?



### 解答1

​	第一种最简单的方式就是直接遍历序列的长度加一的列表，假如i不在nums列表中，返回i即可，但是时间超时。

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        if len(nums)==0:
            return 0
        
        for i in range(len(nums)+1):
            if i not in nums:
                return i
        return 0
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	第二种解答就是可以先计算序列0-n这个等差数列的和(0+1+2+…+n=n*(n+1)/2)，然后用这个和依次减去nums中的数字，剩下就是那个数字了。

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        if len(nums)==0:
            return 0
        sums = len(nums)*(len(nums)+1)//2
        for num in nums:
            sums-=num
        return sums
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答3

​	第三种解法是先把list排序，然后遍历index和value，假如不相等就返回，最后要考虑n不在的情况。

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        if len(nums)==0:
            return 0
        nums.sort()
        for i,num in enumerate(nums):
            if num!=i:
                return i
        return i+1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答4

​	第四种就比较巧妙了，还记得之前做single_number的时候使用异或来找出只出现一次的元素，那么我们也可以使用这种方式，怎么构造呢，把index加进来做异或就ok了。看下面的表格应该很清楚了，但是也要注意最后一个元素的情况。

| index | 0    | 1    | 2    |
| ----- | ---- | ---- | ---- |
| value | 0    | 1    | 3    |

```python
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        if len(nums)==0:
            return 0
        miss = len(nums)
        for i,num in enumerate(nums):
            miss ^= i
            miss ^= num
        return miss
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 