## 022.Generate Parentheses

### 题目描述

给出 *n* 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且**有效的**括号组合。

例如，给出 *n* = 3，生成结果为：

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

### 解答1

​	这道题和前面的括号判别有一定的相似之处，但是这道题需要生成符合规范的字符串，可以分解成两个步骤，首先生成所有可能的结果，然后判别这些字符串是否符合规范即可。这样自然是暴力法解决问题，注意这里使用了递归的方法来生成所有的字符串。

```python
class Solution:
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        def generate(A=[]):
            
            if len(A)==2*n:
                if valid(A):
                    ans.append(''.join(A))
            else:
                A.append('(')
                generate(A)
                A.pop()
                A.append(')')
                generate(A)
                A.pop()
                
        
        def valid(A):
            flag = 0
            for c in A:
                if c =='(':
                    flag += 1
                else:
                    flag -= 1
                if flag <0:
                    return False
            return flag == 0
            
        ans = []
        generate()
        return ans
```

- 时间复杂度：$O(2^{2n}n)$
- 空间复杂度：$O(2^{2n}n)$

### 解答2

​	优化暴力法的方法是回溯法，也就是我们知道序列仍然有效时才去添加"("或者")"，而不是每一次都去添加，可以通过跟踪到目前为止放置的左括号和右括号的数目来做到这一点，如果我们还剩一个位置，我们可以开始放一个左括号。 如果它不超过左括号的数量，我们可以放一个右括号。

```python
class Solution:
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        ans = []
        def generate(A='',left=0,right=0):
            if len(A)==2*n:
                ans.append(A)
                return
            if left < n:
                generate(A+'(',left+1,right)
            if right < left:
                generate(A+')',left,right+1)
        
        generate()
        return ans
```

- 时间复杂度：$O(\frac{4^n}{\sqrt{n}})$
- 空间复杂度：$O(\frac{4^n}{\sqrt{n}})$ 