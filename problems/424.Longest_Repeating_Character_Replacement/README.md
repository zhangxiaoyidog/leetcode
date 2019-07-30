## 424.Longest Repeating Character Replacement

## 题目描述

给你一个仅由大写英文字母组成的字符串，你可以将任意位置上的字符替换成另外的字符，总共可最多替换 k 次。在执行上述操作后，找到包含重复字母的最长子串的长度。

**注意:**
字符串长度 和 k 不会超过 104。

**示例 1:**

```
输入:
s = "ABAB", k = 2

输出:
4

解释:
用两个'A'替换为两个'B',反之亦然。
```


**示例 2:**

```
输入:
s = "AABABBA", k = 1

输出:
4

解释:
将中间的一个'A'替换为'B',字符串变为 "AABBBBA"。
子串 "BBBB" 有最长重复字母, 答案为 4。
```



### 解答

​	这道题还是采用滑动窗口的思想，也是和[209](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/209.Minimum_Size_Subarray_Sum/README.md)题同一个思想，先利用set去重，然后对于每一个字母，我们利用一个滑动窗口向前遍历，先窗口右端向前滑动，遇到不同的字母count就加一，表示要替换成这个字母，直到count到到最大替换次数，然后窗口的左端再往前滑，直到把count减回k以内，最后求出每个字母的最大窗口值就好了。

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        res = 0
        for c in set(s):
            start, end, length, count = 0, 0, 0, 0
            # 滑动窗口
            while end<len(s):
                if s[end]!=c:
                    count+=1
                end+=1
                
                while count>k:
                    if s[start]!=c:
                        count-=1
                    start+=1
                length = max(length, end-start)
            res = max(res, length)
        return res
```

- 时间复杂度：$O(m*n)(m为不同的字母数，n为字符长度)$
- 空间复杂度：$O(1)$	