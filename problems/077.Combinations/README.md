## 077.Combinations

### 题目描述

给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。

**示例:**

```
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

### 解答

​	这个问题我一开始还是没办法解出来的，因为这一类问题总结的比较少吧，在数学的集合问题里面经常出现需要求解幂集、排列数、组合数这一类的问题，对于这一类的问题，我觉得应该都是可以使用递归来实现的。在参考了discuss的答案后，得出了问题的一种解答：每次固定住最大的，然后从剩下的去选，当选定一个最大值时就可以使用递归去求解这个问题了。

​	递归的关键在于两点，第一是如何让去缩小问题的规模，即使用相同的手段去求解不同规模的子问题；第二就是当问题小到一定的规模的时候，就可以得到此时的一个解，也就是递归的出口，其实递归的过程和栈的使用有些相似，调用递归方法相当于入栈，找到出口的时候就相当于出栈。



```python
class Solution:
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        ans = []
        temp = []
        self.rec_combine(ans,temp,n,k)
        return ans
        
    
    def rec_combine(self,ans,temp,n,k):
        # 递归求解，每次固定住最大的
        
        if k==0:
            ans.append(list(temp))
        else:
            for i in range(n,0,-1):
                temp.append(i)
                self.rec_combine(ans,temp,i-1,k-1)
                temp.remove(i)
```

