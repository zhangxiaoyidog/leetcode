## 020.Valid Parentheses

### 题目描述

给定一个只包括 `'('`，`')'`，`'{'`，`'}'`，`'['`，`']'` 的字符串，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

**示例 1:**

```
输入: "()"
输出: true
```

**示例 2:**

```
输入: "()[]{}"
输出: true
```

**示例 3:**

```
输入: "(]"
输出: false
```

**示例 4:**

```
输入: "([)]"
输出: false
```

**示例 5:**

```
输入: "{[]}"
输出: true
```



### 解答

​	这道题是一道简单题，以前学习数据结构的时候就有遇到过类似的题目，在这道题目中是要判断括号的闭合成对出现，这样就可以使用栈来帮组我们解题，遍历字符串，左括号进栈，右括号出栈与当前字符比较，成对则继续，否则直接返回False，直到遍历完成，关键在于程序能否判断左括号数量不等于右括号数量这两种情况(大于或小于)，实现起来也比较简单。

```python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # 使用栈来帮助解题
        stack = []
        flag = 1
        for i in s:
            if i=='(' or i =='[' or i =='{':
                stack.append(i)
            else:
                if len(stack) == 0:
                    flag = 0
                    break
                temp = stack.pop()
                if temp + i!='()' and temp + i!='[]' and temp + i!='{}':
                    flag = 0
                    break
        if len(stack) != 0 or flag == 0:
            return False
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 