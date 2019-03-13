## 151.Reverse Words in a String

## 题目描述

给定一个字符串，逐个翻转字符串中的每个单词。

 

**示例 1：**

```
输入: "the sky is blue"
输出: "blue is sky the"
```

**示例 2：**

```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

**示例 3：**

```
输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```

 

**说明：**

- 无空格字符构成一个单词。
- 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
- 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。



### 解答

​	这道题我的思路就是遍历一遍字符串，遇到字母就合并到另一个字符串中，遇到空格则把上一个字符串insert到一个list第一个位置，最后把list用join方法串起来。这里面有一些细节就是最后一个字符串要单独处理，然后多个空格的情况要判断。

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        if len(s) == 0:
            return s
        i = 0
        temp = ''
        res = []
        while i < len(s):
            if s[i] != ' ':
                temp+=s[i]
            # 多空格的情况这里可以处理掉
            elif len(temp) != 0:
                res.insert(0, temp)
                temp = ''
            i += 1
        #　处理最后一个字母
        if len(temp) != 0:
            res.insert(0, temp)
        return ' '.join(res)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$