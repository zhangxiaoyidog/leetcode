## 345.Reverse Vowels of a String

## 题目描述

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

**示例 1:**

```
输入: "hello"
输出: "holle"
```

**示例 2:**

```
输入: "leetcode"
输出: "leotcede"
```


**说明:**
元音字母不包含字母"y"。



### 解答

```python
class Solution(object):
    def reverseVowels(self, s):
        """
        :type s: str
        :rtype: str
        """
        target = ['a','e','i','o','u','A', 'E', 'I', 'O', 'U']
        s = list(s)
        start = 0
        end = len(s)-1

        while start<end:
            if s[start] in target and s[end] in target:
                s[start],s[end] = s[end],s[start]
                start+=1
                end-=1
            if s[start] not in target:
                start+=1
            if s[end]  not in target:
                end-=1   
            # while s[start] not in target and start<end:
            #     start+=1
            # while s[end] not in target and start<end:
            #     end-=1
            # if start<end:
            #     s[start],s[end] = s[end],s[start]
            #     start+=1
            #     end-=1
        return ''.join(s)
```

- 时间复杂度：$O(n)​$
- 空间复杂度：$O(1)$ 