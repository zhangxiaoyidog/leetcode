## 402.Remove K Digits

### 题目描述

给定一个以字符串表示的非负整数 num，移除这个数中的 k 位数字，使得剩下的数字最小。

**注意:**

```
num 的长度小于 10002 且 ≥ k。
num 不会包含任何前导零。
```

**示例 1 :**

```
输入: num = "1432219", k = 3
输出: "1219"
解释: 移除掉三个数字 4, 3, 和 2 形成一个新的最小的数字 1219。
```

**示例 2 :**

```
输入: num = "10200", k = 1
输出: "200"
解释: 移掉首位的 1 剩下的数字为 200. 注意输出不能有任何前导零。
```

**示例 3 :**

```
输入: num = "10", k = 2
输出: "0"
解释: 从原数字移除所有的数字，剩余为空就是0。
```



### 解答

​	这道题如果直接移除数字感觉是很费事，所以需要转化成从整数中找到len(num)-k个数字的问题，比如num = "1432219", k = 3，第一个数字必须从0\~3中选，因为若选了第四个或者之后的数字后面的就不够了，第二个数字从1\~4中选，以此类推，第i个数字的取值范围(i-1, k + count)，每次选都选最小的即可。

```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        # 转成从整数中找到len(num)-k个数字的问题
        count = 0
        left = len(num) - k
        start = 0
        res = ''
        # 第i个数字的取值范围(i-1, k + count)
        while count < left:
            min_i = 0
            min_v = float('inf')
            print(start, k + count + 1)
            for i in range(start, k + count + 1):
                if int(num[i]) < min_v:
                    min_i = i
                    min_v = int(num[i])

            res += num[min_i]
            start = min_i + 1
            # print(min_i, start)
            count += 1

        if len(res) == 0:
            return '0'
        return str(int(res))
```

- 时间复杂度：$O(n*k)$
- 空间复杂度：$O(k)$ 