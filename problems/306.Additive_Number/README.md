## 306.Additive Number

## 题目描述

累加数是一个字符串，组成它的数字可以形成累加序列。

一个有效的累加序列必须**至少**包含 3 个数。除了最开始的两个数以外，字符串中的其他数都等于它之前两个数相加的和。

给定一个只包含数字 `'0'-'9'` 的字符串，编写一个算法来判断给定输入是否是累加数。

**说明:** 累加序列里的数不会以 0 开头，所以不会出现 `1, 2, 03` 或者 `1, 02, 3` 的情况。

**示例 1:**

```
输入: "112358"
输出: true 
解释: 累加序列为: 1, 1, 2, 3, 5, 8 。1 + 1 = 2, 1 + 2 = 3, 2 + 3 = 5, 3 + 5 = 8
```

**示例 2:**

```
输入: "199100199"
输出: true 
解释: 累加序列为: 1, 99, 100, 199。1 + 99 = 100, 99 + 100 = 199
```

**进阶:**
你如何处理一个溢出的过大的整数输入?



### 解答

​	这道题只需要判断是否构成即可，所以采用回溯法来解决，也就是使用dfs寻找符合条件的数字切片，判断切片是否满足条件，在回溯时判断数组的长度是否大于等于3，假如超过则判断是否满足最后的数字等于它前面两个数字的和，不超过3或者满足条件的条件继续递归，最后当所有的字符串被切片完毕，要判断下数组长度是否大于等于3。

```python
class Solution:
    def isAdditiveNumber(self, num: str) -> bool:
        def dfs(results,result,candidates,k):
            if len(results) > 2 and results[-1] != results[-2]+results[-3]:
                return False
            if k == len(candidates) and len(results) >= 3:
                return True
            
            for i in range(k,len(candidates)):
                # 序列不能以0开头
                if candidates[k] == '0' and i > k:
                    print('1111111')
                    return False
                result += candidates[i]
                results.append(int(result))
                if dfs(results,'',candidates,i+1):
                    return True
                results.pop()
            return False
                
        results = []
        return dfs(results,'',num,0)
```



