## 295.Find Median from Data Stream

## 题目描述

中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

- void addNum(int num) - 从数据流中添加一个整数到数据结构中。
- double findMedian() - 返回目前所有元素的中位数。

**示例：**

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```

**进阶:**

1. 如果数据流中所有整数都在 0 到 100 范围内，你将如何优化你的算法？
2. 如果数据流中 99% 的整数都在 0 到 100 范围内，你将如何优化你的算法？



### 解答

​	这道题就是add的时候假如直接线性查找插入点是会超时的，这里也可以看出来是一个查找问题，并且还是有序的，所以可以用二分查找去找查找位置。

```python
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.nums = []
        

    def addNum(self, num: int) -> None:
        if len(self.nums)==0 or self.nums[-1]<=num:
            self.nums.append(num)
            return
        elif self.nums[0]>=num:
            self.nums.insert(0, num)
            return
        else:
            # 二分查找找插入点
            left = 0
            right = len(self.nums)-1
            while left<right:
                mid = (left+right)//2
                if self.nums[mid] > num:
                    right = mid
                else:
                    left = mid + 1
            self.nums.insert(left, num)
        return 
    def findMedian(self) -> float:
        if len(self.nums)%2==1:
            return self.nums[len(self.nums)//2]
        else:
            return (self.nums[len(self.nums)//2] + self.nums[len(self.nums)//2-1])/2




# Your MedianFinder object will be instantiated and called as such:
# obj = MedianFinder()
# obj.addNum(num)
# param_2 = obj.findMedian()
```

