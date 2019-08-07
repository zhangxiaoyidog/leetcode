## 873.Length of Longest Fibonacci Subsequence

## 题目描述

如果序列 X_1, X_2, ..., X_n 满足下列条件，就说它是 斐波那契式 的：

+ n >= 3
+ 对于所有 i + 2 <= n，都有 X_i + X_{i+1} = X_{i+2}

给定一个严格递增的正整数数组形成序列，找到 A 中最长的斐波那契式的子序列的长度。如果一个不存在，返回  0 。

（回想一下，子序列是从原序列 A 中派生出来的，它从 A 中删掉任意数量的元素（也可以不删），而不改变其余元素的顺序。例如， [3, 5, 8] 是 [3, 4, 5, 6, 7, 8] 的一个子序列）

 

**示例 1：**

```
输入: [1,2,3,4,5,6,7,8]
输出: 5
解释:
最长的斐波那契式子序列为：[1,2,3,5,8] 。
```


**示例 2：**

```
输入: [1,3,7,11,12,14,18]
输出: 3
解释:
最长的斐波那契式子序列有：
[1,11,12]，[3,11,14] 以及 [7,11,18] 。
```






**提示：**

+ 3 <= A.length <= 1000
+ 1 <= A[0] < A[1] < ... < A[A.length - 1] <= 10^9
+ （对于以 Java，C，C++，以及 C# 的提交，时间限制被减少了 50%）



### 解答1

​	第一种解法比较容易想到的是暴力解，首先确定两个数字，然后往前搜索是否还有后面的数字。

```python
class Solution:
    def lenLongestFibSubseq(self, A: List[int]) -> int:
        res = 0
        nums = set(A)
        # 暴力
        for i in range(len(A)):
            for j in range(i+1,len(A)):
                l = 2
                a,b =A[j], A[i] + A[j]
                while b in nums:
                    l += 1
                    a,b = b,a+b
                res = max(res,l)
        return res if res>=3 else 0
```

- 时间复杂度：$O(n^3)$
- 空间复杂度：$O(n)$ 



### 解答2

​	其实我们的暴力解里面有很多情况是重复判断了，我们用dp[(A[j],A[i])]表示以A[j]，A[i]结尾的斐波那契数列的长度，假如A[i]-A[j]在nums中，说明至少可以组成一个长度为3的数列，并且dp[(A[j],A[i])] = dp.get((A[i]-A[j],A[j]), 2) +1。

```python
class Solution:
    def lenLongestFibSubseq(self, A: List[int]) -> int:
        # 动态规划 dp[(A[j],A[i])]表示以A[j]，A[i]结尾的斐波那契数列的长度
        
        dp = {}
        nums = set(A)
        for i in range(len(A)):
            for j in range(i):
                if A[i] - A[j] < A[j] and A[i]-A[j] in nums:
                    dp[(A[j],A[i])] = dp.get((A[i]-A[j],A[j]), 2) +1
        if len(dp)==0:
            return 0
        return max(dp.values())
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$ 