## 394.Decode String

### 题目描述

给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。

**示例:**

```
s = "3[a]2[bc]", 返回 "aaabcbc".
s = "3[a2[c]]", 返回 "accaccacc".
s = "2[abc]3[cd]ef", 返回 "abcabccdcdcdef".
```



### 解答1

​	使用两个栈，遍历s过程中，假如不是']'，则依次入栈1，如果是'['，则记录下它的位置入栈2，如果当前元素是数字，则要看前面一个元素，因为数字有可能会大于9，是的话就需要连成一个数字，字母则就直接入栈了。如果遇到']'，则弹出栈2的栈顶元素得到上一个'['的对应位置，将'[]'中的元素乘上倍数放入栈1中，代码有一个疑问是假如乘上倍数后字符串的长度长于栈的长度了，最后那一段赋值语句也不会出错，因为list会自动往后延，这就是python的魔力了。

```python
class Solution:
    def decodeString(self, s: str) -> str:
        
        stack = []
        index = []
        
        for c in s:
            if c!=']':
                if c=='[':
                    index.append(len(stack))
                    stack.append(c)
                # 数字大于9
                elif len(stack)>0 and c.isdigit() and stack[-1].isdigit():
                    stack[-1]+=c
                else:
                    stack.append(c)
            else:
                ix = index.pop()
                stack[ix-1:] = int(stack[ix-1])*stack[ix+1:]
                
        return ''.join(stack)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 



### 解答2

​	第二种是只用一个栈，非']'就入栈，是'['就把入栈的字符串弹出来处理。当然包括前面也入栈了的'['，处理的时候忽略即可，然后乘以倍数再考虑是否入栈，因为可能有嵌套的情况，最后返回时记得加上重复一次，也就是没有[]夹住的情况。

```python
class Solution:
    def decodeString(self, s: str) -> str:

        stack = []
        res = ''
        for i, c in enumerate(s):
            if c!=']':
                stack.append(c)
            else:
                string = ''
                # 得到当前要处理的字符串
                while not stack[-1].isdigit():
                    string = stack.pop() + string
                times = ''
                while stack and stack[-1].isdigit():
                    times = stack.pop() + times

                if times:
                    string = int(times) * string[1:]
                if stack:
                    stack.append(string)
                else:
                    res += string
        # 可能还有未处理完的
        return res+''.join(stack)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 



