## 421.Maximum XOR of Two Numbers in an Array

## 题目描述

给定一个非空数组，数组中元素为 a0, a1, a2, … , an-1，其中 0 ≤ ai < 231 。

找到 ai 和aj 最大的异或 (XOR) 运算结果，其中0 ≤ i,  j < n 。

你能在O(n)的时间解决这个问题吗？

**示例:**

```
输入: [3, 10, 5, 25, 2, 8]

输出: 28

解释: 最大的结果是 5 ^ 25 = 28.
```



### 解答1

​	暴力遍历所有的可能。

```python
class Solution:
    def findMaximumXOR(self, nums: List[int]) -> int:
        # 暴力解答
        res = 0
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                res = max(res,nums[i]^nums[j])
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$	



### 解答2

​	使用贪心的策略，由于如果 a ^ b = c 成立，那么a ^ c = b 与 b ^ c = a 均成立。那么可以从最高为1的位置开始，贪心地认为这一位是1，再把当前得到的数与这个 n 个数的 前缀（因为是从高位到低位看，所以称为“前缀”）进行异或运算，放在一个哈希表中，再依次把所有前缀与这个假设的“最大值”进行异或以后得到的结果放到哈希表里查询一下，如果查得到，就说明这个数位上可以是“1”，否则就只能是 0。

```python
class Solution:
    def findMaximumXOR(self, nums: List[int]) -> int:
        res = 0
        mask = 0
        
        for i in range(31,-1,-1):
            mask |= (1<<i)
            # 这一轮的所有前缀
            s = set()
            
            for num in nums:
                s.add(mask & num)
            # 贪心认为这一位可以是1，然后去做亦或
            temp = res | (1<<i)
            
            for prefix in s:
                if temp ^ prefix in s:
                    res = temp

                    break
        return res
```

- 时间复杂度：$O(n*32)$
- 空间复杂度：$O(n)$



