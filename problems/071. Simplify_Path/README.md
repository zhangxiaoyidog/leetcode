## 071.Simplify Path

### 题目描述

给定一个文档 (Unix-style) 的完全路径，请进行路径简化。

例如，
**path** = `"/home/"`, => `"/home"`
**path** = `"/a/./b/../../c/"`, => `"/c"`

**边界情况:**

- 你是否考虑了 路径 = `"/../"` 的情况？
  在这种情况下，你需返回 `"/"` 。
- 此外，路径中也可能包含多个斜杠 `'/'` ，如 `"/home//foo/"` 。
  在这种情况下，你可忽略多余的斜杠，返回 `"/home/foo"` 。



### 解答

​	这道题的关键点有两个，首先要想到使用栈这种数据结构来帮助解题，因为后进先出的特点正好能够用来解这一类的题目，诶是不是和之前的括号匹配相似，问题的本质是一样的，然后第二个点是要想到怎么配合栈的使用，所以我们要先利用‘/’把字符串给分开，然后一一进栈，路径中的..，实际上就是将目录回退一格，那被回退的目录是哪一个呢？是后面进来的那个目录，这种场景也是符合后进先出的。

```python
class Solution:
    def simplifyPath(self, path):
        """
        :type path: str
        :rtype: str
        """
        if len(path)==0:
            return None
        if len(path)==1:
            return path
        stack = []
        phs = path.split('/')
    
        for ph in phs:
            if ph=='..':
                # 弹出
                if len(stack)!=0:
                    stack.pop()
            elif ph!='.' and ph !='':
                # 进栈
                stack.append(ph)
        
        return '/'+'/'.join(stack)
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

