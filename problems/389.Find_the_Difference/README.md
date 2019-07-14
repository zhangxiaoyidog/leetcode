## 389.Find the Difference

### 题目描述

给定两个字符串 s 和 t，它们只包含小写字母。

字符串 t 由字符串 s 随机重排，然后在随机位置添加一个字母。

请找出在 t 中被添加的字母。

 

**示例:**

```
输入：
s = "abcd"
t = "abcde"

输出：
e

解释：
'e' 是那个被添加的字母。
```



### 解答1

​	使用一个字典存储原字符串中每个字符的出现个数，然后遍历第二个字符串的时候可以从个数是否为0或者是否在字典中来判断是否是新添加的字母。

```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        res = {}
        for c in s:
            res[c] = res.get(c,0)+1
        for c in t:
            if c not in res or res[c]==0:
                return c
            res[c]-=1
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 



### 解答2

​	在遍历字符串时可以把每个字符的ascii码叠加，然后减去第二个字符串的每一个字符的ascii码叠加，就可以得到被添加的字母了。

```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        a, b = 0, 0
        for c in s:
            a+=ord(c)
        for c in t:
            b+=ord(c)
        return chr(b-a)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

