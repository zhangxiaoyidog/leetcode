## 215.Kth_Largest_Element_in_an_Array

## 题目描述

在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例 1:**

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

**说明:**

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。



### 解答

​	这道题要找到第k大的元素，其实最直观的方式就是使用堆排序了，维护一个大根堆，然后每次把最大的提出来，调整堆最后得到第k大的就可以了，但是这里也可以使用快速排序的思想，每次去找一个基准，一次排序后它肯定在第m大的位置上，这时候只需要判断m是否跟k相等就可以了，如果小于k，那么就去前半段继续使用快排，否则去后半段找。

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        return self.quick_search(nums,0,len(nums)-1,k)
    
    def quick_search(self,nums,start,end,k):
        def swap(nums,i,j):
            temp = nums[i]
            nums[i] = nums[j] 
            nums[j] = temp
        
        if start > end:
            return 0
        left = start
        privot = nums[end]
        
        for i in range(start,end):
            if nums[i] >= privot:
                swap(nums,left,i)
                left+=1
        swap(nums,left,end)
        
        if left==k-1:
            # print(left,nums)
            return nums[left]
        elif left<k-1:
            return self.quick_search(nums,left+1,end,k)
        else:
            return self.quick_search(nums,start,left-1,k)
```

