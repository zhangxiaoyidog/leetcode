## 347.Top K Frequent Elements

## 题目描述

给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```


**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```


**说明：**

+ 你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
+ 你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。



### 解答

​	这道题我是用了python内置函数sorted排序的，首先建立一个数字及其出现次数一一对应dict，然后根据频数排序，最后找出前k个。其实要求的做法应该是使用堆排序的方式，首先还是使用哈希表对每个元素出现的次数进行统计，然后根据元素出现次数进行排序处理，需要维护一个大顶堆。

```python
class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        dic = {}
        for num in nums:
            if num in dic:
                dic[num] += 1
            else:
                dic[num] = 1
        # 根据频数排序
        r = sorted(dic.items(), key=lambda d:d[1], reverse=True)
        res = []
        # print(r)
        for item in r:
            if k>0:
                k-=1
                res.append(item[0])
            else:
                break
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 