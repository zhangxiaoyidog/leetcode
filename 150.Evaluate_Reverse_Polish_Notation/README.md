## 150.Evaluate Reverse Polish Notation

## 题目描述

根据[逆波兰表示法](https://baike.baidu.com/item/%E9%80%86%E6%B3%A2%E5%85%B0%E5%BC%8F/128437)，求表达式的值。

有效的运算符包括 `+`, `-`, `*`, `/` 。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

**说明：**

- 整数除法只保留整数部分。
- 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。

**示例 1：**

```
输入: ["2", "1", "+", "3", "*"]
输出: 9
解释: ((2 + 1) * 3) = 9
```

**示例 2：**

```
输入: ["4", "13", "5", "/", "+"]
输出: 6
解释: (4 + (13 / 5)) = 6
```

**示例 3：**

```
输入: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
输出: 22
解释: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22
```



### 解答

​	这道题在以前学习数据结构的时候就经常会遇见，是一个比较经典的使用栈来解题的题目，使用if判断然后计算，不过计算除法的时候这里要求向下取整，要注意一下，在评论区也看到了使用lambda表达式，那确实是Pythonic！！！

```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        # 使用栈解题
        stack = []
        for token in tokens:
            if token.isdigit() or len(token)>1:
                stack.append(int(token))
            else:
                a = stack.pop(-1)
                b = stack.pop(-1)
                if token == '+':
                    stack.append(a+b)
                if token == '-':
                    stack.append(b-a)
                if token == '*':
                    stack.append(a*b)
                if token == '/':
                    # 这里要注意向下取整
                    stack.append(int(b/a))
        return stack[0]
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

