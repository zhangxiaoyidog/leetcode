## 076.Minimum Window Substring

### 题目描述

给你一个字符串 S、一个字符串 T，请在字符串 S 里面找出：包含 T 所有字母的最小子串。

**示例：**

```
输入: S = "ADOBECODEBANC", T = "ABC"
输出: "BANC"
```

**说明：**

+ 如果 S 中不存这样的子串，则返回空字符串 ""。
+ 如果 S 中存在这样的子串，我们保证它是唯一的答案。



### 解答

​	我是做了[438](https://github.com/zhangxiaoyidog/leetcode/tree/master/problems/438.Find_All_Anagrams_in_a_String)题才返回来做的这道题，当初看这道题还是很有难度的，因为没做过滑动窗口的题目，还是使用滑动窗口的思想，不断增加right 指针扩大窗口 [left, right]，直到窗口中的字符串符合要求（包含了 T 中的所有字符），然后停止增加right，不断增加left取缩小窗口，直到窗口的字符串不再符合要求，每次增加left，都要更新res，就这样直到end走到头，这个题比438题难的地方在于窗口中可能还会出现其他的字符，以及需要的字符可能出现次数会大于1，需要一些小技巧直接看代码即可。

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if s == t:
            return s
        need = {}
        for c in t:
            need[c] = need.get(c, 0) + 1

        start, end = 0, 0
        res = ''
        windows = {}
        match = 0
        while end < len(s):
            if s[end] in need:
                windows[s[end]] = windows.get(s[end], 0) + 1
                if windows[s[end]] == need[s[end]]:
                    # 字符s[end]的出现次数符合要求了
                    match += 1
            # 已经符合要求了
            while match == len(need):
                # start更新后也要更新res
                if res == '' or end - start + 1 < len(res):
                    res = s[start:end + 1]
                if s[start] in windows:
                    windows[s[start]] -= 1
                    if windows[s[start]] < need[s[start]]:
                        match -= 1
                start += 1
            end += 1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 