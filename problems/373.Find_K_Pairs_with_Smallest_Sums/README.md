## 373.Find K Pairs with Smallest Sums

### 题目描述

给定两个以升序排列的整形数组 nums1 和 nums2, 以及一个整数 k。

定义一对值 (u,v)，其中第一个元素来自 nums1，第二个元素来自 nums2。

找到和最小的 k 对数字 (u1,v1), (u2,v2) ... (uk,vk)。

**示例 1:**

```
输入: nums1 = [1,7,11], nums2 = [2,4,6], k = 3
输出: [1,2],[1,4],[1,6]
解释: 返回序列中的前 3 对数：
     [1,2],[1,4],[1,6],[7,2],[7,4],[11,2],[7,6],[11,4],[11,6]
```


**示例 2:**

```
输入: nums1 = [1,1,2], nums2 = [1,2,3], k = 2
输出: [1,1],[1,1]
解释: 返回序列中的前 2 对数：
     [1,1],[1,1],[1,2],[2,1],[1,2],[2,2],[1,3],[1,3],[2,3]

```


**示例 3:**

```
输入: nums1 = [1,2], nums2 = [3], k = 3 
输出: [1,3],[2,3]
解释: 也可能序列中所有的数对都被返回:[1,3],[2,3]
```



### 解答

​	这个问题是取任意组合两个数字后的和最小的k对数字，一开始我是想用两个指针分别从两个数字的第一个数字开始出发，然后从小到大取，但是这样会漏掉一些数字对，因为有可能一个指针没走到头另一个就开始走了，那么第一个指针后面的数字和第二个指针前面的数字的组合就取不到了，所以需要换一种思路。

​	我们可以维护一个小根堆，每次取堆顶和最小的那对组合就好了，首先先把nums1的第一个元素和nums2的所有元素的组合建立堆，然后把最小和的元素对弹出，把最小元素对[a,b]中的a所对应的nums1的元素下标加1和b组合继续加入堆中，一直到组合完毕。

```python
import heapq
class Solution:
    def kSmallestPairs(self, nums1: List[int], nums2: List[int], k: int) -> List[List[int]]:
        res = []
        if len(nums1)==0 or len(nums2)==0 or k==0:
            return res
        heap = [[nums1[0]+nums2[i],0,i] for i in range(len(nums2))]
        # 利用堆每次取最小的
        while k and heap:
            val,i,j = heapq.heappop(heap)
            res.append([nums1[i],nums2[j]])
            if i < len(nums1)-1:
                heapq.heappush(heap,[nums1[i+1]+nums2[j],i+1,j])
            k-=1
        return res
```

- 时间复杂度：$O(m*n)$
- 空间复杂度：$O(k)$ 

