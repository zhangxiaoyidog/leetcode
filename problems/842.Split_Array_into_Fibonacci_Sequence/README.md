## 842.Split Array into Fibonacci Sequence

## 题目描述

给定一个数字字符串 S，比如 S = "123456579"，我们可以将它分成斐波那契式的序列 [123, 456, 579]。

形式上，斐波那契式序列是一个非负整数列表 F，且满足：

+ 0 <= F[i] <= 2^31 - 1，（也就是说，每个整数都符合 32 位有符号整数类型）；
+ F.length >= 3；
+ 对于所有的0 <= i < F.length - 2，都有 F[i] + F[i+1] = F[i+2] 成立。

另外，请注意，将字符串拆分成小块时，每个块的数字一定不要以零开头，除非这个块是数字 0 本身。

返回从 S 拆分出来的所有斐波那契式的序列块，如果不能拆分则返回 []。

**示例 1：**

```
输入："123456579"
输出：[123,456,579]
```

**示例 2：**

```
输入: "11235813"
输出: [1,1,2,3,5,8,13]
```

**示例 3：**

```
输入: "112358130"
输出: []
解释: 这项任务无法完成。
```

**示例 4：**

```
输入："0123"
输出：[]
解释：每个块的数字不能以零开头，因此 "01"，"2"，"3" 不是有效答案。
```

**示例 5：**

```
输入: "1101111"
输出: [110, 1, 111]
解释: 输出 [11,0,11,11] 也同样被接受。
```

**提示：**

1. 1 <= S.length <= 200
2. 字符串 S 中只含有数字。

### 解答

​	这道题和ip切分的那道题有点相似，都是采用dfs求解，这里要注意剪枝和边界判断。

```python
class Solution:
    def splitIntoFibonacci(self, S ) :
        def dfs_search(results, result, k, S):
            if len(result) > 2 and result[-1] != result[-2] + result[-3]:
                return False
            if k == len(S) and len(result) > 2:
                results.append(list(result))
                return
            temp_num = ''
            for i in range(k, len(S)):
                temp_num += S[i]
                if temp_num[0] == '0' and len(temp_num)!=1:
                    continue
                if int(temp_num) > 2147483647:
                    continue
                dfs_search(results,result + [int(temp_num)], i + 1, S)
            return
        results = []
        dfs_search(results,[], 0, S)
        # print results
        return results[0] if len(results)>0 else []
```

