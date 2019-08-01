## 438.Find All Anagrams in a String

## 题目描述

给定一个字符串 s 和一个非空字符串 p，找到 s 中所有是 p 的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 s 和 p 的长度都不超过 20100。

**说明：**

+ 字母异位词指字母相同，但排列不同的字符串。
+ 不考虑答案输出的顺序。

**示例 1:**

```
输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
```


 **示例 2:**

```
输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]

解释
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。
```



### 解答

​	这道题还是用滑动窗口往前滑动，由于是找几个字母的异味词，那么可以不用管顺序，只需要字母的数目对的上即可，一开始我是每次窗口滑动一下就遍历整个窗口的值，提交超时，其实只需要把更新的头尾的那两个字母修改次数即可，可以使用字典，也可以使用python的counter，比较方便。

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        if s==p:
            return [0]
        res = []
        char_map = {}
        for c in p:
            char_map[c] = char_map.get(c, 0) + 1
        start = 0
        end = 0
        maps = {}
        while end<len(s):
            maps[s[end]] = maps.get(s[end],0) + 1
            if end-start==len(p)-1:
                if maps==char_map:
                    res.append(start)
                maps[s[start]]-=1
                # 变为0了要删除，要不后面的判断会出错
                if maps[s[start]] == 0:
                    del maps[s[start]]
                start+=1
            end+=1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$