## 087.Scramble String

### 题目描述

给定一个字符串 *s1*，我们可以把它递归地分割成两个非空子字符串，从而将其表示为二叉树。

下图是字符串 *s1* = `"great"` 的一种可能的表示形式。

```
    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t
```

在扰乱这个字符串的过程中，我们可以挑选任何一个非叶节点，然后交换它的两个子节点。

例如，如果我们挑选非叶节点 `"gr"` ，交换它的两个子节点，将会产生扰乱字符串 `"rgeat"` 。

```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t
```

我们将 `"rgeat”` 称作 `"great"` 的一个扰乱字符串。

同样地，如果我们继续将其节点 `"eat"` 和 `"at"` 进行交换，将会产生另一个新的扰乱字符串 `"rgtae"` 。

```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a
```

我们将 `"rgtae”` 称作 `"great"` 的一个扰乱字符串。

给出两个长度相等的字符串 *s1* 和 *s2*，判断 *s2* 是否是 *s1* 的扰乱字符串。

**示例 1:**

```
输入: s1 = "great", s2 = "rgeat"
输出: true
```

**示例 2:**

```
输入: s1 = "abcde", s2 = "caebd"
输出: false
```



### 解答

​	这道题要判断两个字符串是否满足‘扰乱’关系，那就用递归去判断S1的左子树和S2的左子树是否能满足且S1的右子树和S2的右子树是否满足，或者S1的左子树和S2的右子树是否能满足且S1的右子树和S2的左子树是否满足这种关系即可。

```python
from collections import Counter
class Solution:
    def isScramble(self, s1, s2):
        """
        :type s1: str
        :type s2: str
        :rtype: bool
        """
        
        if s1 == s2:
            return True
        # 判断他们的元素是否相等
        if Counter(s1) != Counter(s2):
            return False
        
        for i in range(1,len(s1)):
            
            if self.isScramble(s1[:i],s2[:i]) and self.isScramble(s1[i:],s2[i:]):
                return True
            if self.isScramble(s1[:i],s2[-i:]) and self.isScramble(s1[i:],s2[:-i]):
                return True
        
        return False
```

