## 225.Implement Stack Using Queues

## 题目描述

使用队列实现栈的下列操作：

- push(x) -- 元素 x 入栈
- pop() -- 移除栈顶元素
- top() -- 获取栈顶元素
- empty() -- 返回栈是否为空

**注意:**

- 你只能使用队列的基本操作-- 也就是 `push to back`, `peek/pop from front`, `size`, 和 `is empty` 这些操作是合法的。
- 你所使用的语言也许不支持队列。 你可以使用 list 或者 deque（双端队列）来模拟一个队列 , 只要是标准的队列操作即可。
- 你可以假设所有操作都是有效的（例如, 对一个空的栈不会调用 pop 或者 top 操作）。



### 解答

​	这道题要求使用队列实现栈的操作，那么我们直接使用两个队列来模拟就好了，这里就是入栈的操作比较复杂一点点，每次入栈的时候先把数字入其中一个空队列，然后再把另个一队列的所有元素出队列进另一个队列，这样所有的元素就反过来了，其他的操作就比较简单了。

```python
class MyStack:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.q1 = []
        self.q2 = []
        

    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        if len(self.q1)==0:
            self.q1.append(x)
            for i in range(len(self.q2)):
                self.q1.append(self.q2.pop(0))
        else:
            self.q2.append(x)
            for i in range(len(self.q1)):
                self.q2.append(self.q1.pop(0))

    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        if len(self.q1)!=0:
            return self.q1.pop(0)
        else:
            return self.q2.pop(0)
        
    def top(self) -> int:
        """
        Get the top element.
        """
        if len(self.q1)!=0:
            return self.q1[0]
        else:
            return self.q2[0]

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return len(self.q1)==0 and len(self.q2)==0
        


# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

