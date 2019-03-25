## 169.Majority Element

## 题目描述

给定一个大小为 *n* 的数组，找到其中的众数。众数是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

**示例 1:**

```
输入: [3,2,3]
输出: 3
```

**示例 2:**

```
输入: [2,2,1,1,1,2,2]
输出: 2
```



### 解答1

​	第一种解法是使用字典存储数字出现的个数，最后再排序取出出现最多的数即可。

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        l = len(nums)
        d = {}
        for num in nums:
            if num not in d:
                d[num] = 1
            else:
                d[num] += 1
        d = sorted(d.items(),key=lambda d:d[1])
        return d[-1][0]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$



### 解答2

​	第二种更直接的是把列表排序，然后直接取中间的那个，因为众数是指在数组中出现次数**大于** `⌊ n/2 ⌋` 的元素。

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:    
        nums.sort()
        return nums[len(nums)//2]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$



### 解答

​	第三种就比较巧妙了，被称为摩尔投票算法，算法在局部变量中定义一个序列元素(m)和一个计数器(i)，初始化的情况下计数器为0.  算法依次扫描序列中的元素，当处理元素x的时候，如果计数器为0，那么将x赋值给m，然后将计数器(i)设置为1，如果计数器不为0，那么将序列元素m和x比较，如果相等，那么计数器加1，如果不等，那么计数器减1。处理之后，最后存储的序列元素(m)，就是这个序列中最多的元素。

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:  
        count = 0
        for num in nums:
            if count==0:
                res = num
                count = 1
            elif num == res:
                count+=1
            else:
                count-=1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$