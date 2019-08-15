## 446.Arithmetic Slices II - Subsequence

## 题目描述

如果一个数列至少有三个元素，并且任意两个相邻元素之差相同，则称该数列为等差数列。

例如，以下数列为等差数列:

1, 3, 5, 7, 9
7, 7, 7, 7
3, -1, -5, -9
以下数列不是等差数列。

1, 1, 2, 5, 7


数组 A 包含 N 个数，且索引从 0 开始。该数组子序列将划分为整数序列 (P0, P1, ..., Pk)，P 与 Q 是整数且满足 0 ≤ P0 < P1 < ... < Pk < N。

 

如果序列 A[P0]，A[P1]，...，A[Pk-1]，A[Pk] 是等差的，那么数组 A 的子序列 (P0，P1，…，PK) 称为等差序列。值得注意的是，这意味着 k ≥ 2。

函数要返回数组 A 中所有等差子序列的个数。

输入包含 N 个整数。每个整数都在 -231 和 231-1 之间，另外 0 ≤ N ≤ 1000。保证输出小于 231-1。

 

**示例：**



```
输入：[2, 4, 6, 8, 10]

输出：7

解释：
所有的等差子序列为：
[2,4,6]
[4,6,8]
[6,8,10]
[2,4,6,8]
[4,6,8,10]
[2,4,6,8,10]
[2,6,10]
```



### 解答1

​	这道题比413题难的地方在于子序列可能不是连续位置的，所以最开始想到的是使用dfs去找所有的情况，然后返回长度即可，但是自己写的一开始是先判断当前是否可以组成等差序列再往下递归，但是无法解决重复数字的情况，所以正确的dfs应该是先找递归所有的情况，然后再判断，但是提交超时。

```python
class Solution:
    def numberOfArithmeticSlices(self, A: 'List[int]') -> int:
        # dfs 解法1
        self.res = 0
        self.dfs(A, [], 0)
        return self.res

    def dfs(self, A, temp, start):
        # 这种无法解决出现重复数字的情况
        if len(temp) > 2 and temp not in self.res:
            self.res.append(list(temp))
        if start == len(A):
            return

        self.dfs(A, temp, start + 1)
        if len(temp) < 2:
            self.dfs(A, temp + [A[start]], start + 1)
        else:
            if A[start] - temp[-1] == temp[-1] - temp[-2]:
                self.dfs(A, temp + [A[start]], start + 1)
```



```python
class Solution:
    def numberOfArithmeticSlices(self, A: 'List[int]') -> int:
        # dfs 解法2
        self.res = 0
        self.dfs(A, [], 0)
        return self.res

    def dfs(self, A, temp, start):
        # 这种提交超时
        if start==len(A):
            if len(temp)<3:
                return
            for i in range(1,len(temp)):
                if temp[i] - temp[i - 1] != temp[1] - temp[0]:
                    return
            self.res+=1
            return
        self.dfs(A, temp, start + 1)
        self.dfs(A, temp + [A[start]], start + 1)
```

- 时间复杂度：$O(2^n)$ (数组中的每个元素都可能在或不在子序列中)
- 空间复杂度：$O(n)$



### 解答2

​	还是使用动态规划，只不过这里定义很特殊，由于等差数列的项数至少为3，所以我们用dp\[i][d]代表以 A[i]结束且公差为d的弱等差数列个数。**弱等差数列** 是至少有两个元素的子序列，任意两个连续元素的差相等，那么就可以使用动态转移了，第一个数字前面没有数字，那么它的状态序列自然为空，第二个数字只需要计算和第一个数字的的差然后存入状态即可，那么对于后面的每一个数字，我们可以计算它和它之前的每一个数字a的差d，然后看以a结束且公差为d的弱等差数列个数是多少即可。

```python
class Solution:
    def numberOfArithmeticSlices(self, A: 'List[int]') -> int:
        # 动态规划 dp[i][j]是在A[:i+1]差值为j的所有长度为j的数组数量
        res = 0
        if len(A)<3:
            return 0
        dp=[{} for _ in range(len(A))]
        
        for i in range(1, len(A)):
            for j in range(i):
                diff = A[i]-A[j]
                dp[i][diff] = dp[i].get(diff, 0)+1
                if i > 1 and diff in dp[j]:
                    dp[i][diff]+=dp[j][diff]
                    res+=dp[j][diff]
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n^2)$