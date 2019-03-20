## 155.Min Stack

## 题目描述

设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

- push(x) -- 将元素 x 推入栈中。
- pop() -- 删除栈顶的元素。
- top() -- 获取栈顶元素。
- getMin() -- 检索栈中的最小元素。

**示例:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```



### 解答

​	这道题很简单，就是一些基本操作，这里检索栈中最小元素可以用一个小技巧就是，每次进栈的的元素为当前数字和最小值的元组，也就是进栈时把当前数字和栈顶元组中的第二个元素，也就是前一个最小值比较，比较后再把当前最小值和当前数字一起进栈，那这样我们可以在获取最小元素的时候直接取出，不用每次都去找。

```python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """

        self.stack = []

    def push(self, x: int) -> None:
        if not self.stack:
            self.stack.append((x,x))
        else:
            self.stack.append((x,min(x,self.stack[-1][-1])))
    def pop(self) -> None:
        self.stack.pop(-1)

    def top(self) -> int:
        if len(self.stack)!=0:
            return self.stack[-1][0]

    def getMin(self) -> int:
        return self.stack[-1][-1]



# Your MinStack object will be instantiated and called as such:
# obj = MinStack()
# obj.push(x)
# obj.pop()
# param_3 = obj.top()
# param_4 = obj.getMin()
```

