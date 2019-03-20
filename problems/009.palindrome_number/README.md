## 009 palindrome_number

### 题目描述

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

**示例 1:**

```
输入: 121
输出: true
```

**示例 2:**

```
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
```

**示例 3:**

```
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

## 解答1

​	这道题会受到之前回文序列判断的那道题目的影响，看到题目就会想到把数字转化成字符串来处理，但是代码看起来会很冗余很长，就像下面这样。

```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        flag =1
        if x<0:
            return False
        half_len = len(str(x)) //2
        #判断序列长度为偶数和奇数的两种不同的情况
        if len(str(x)) % 2 == 0:
            x =str(x)
            front = half_len -1
            rear = half_len
            while rear < len(x):
                if x[front]!=x[rear]:
                    flag = 0
                    break
                front-=1
                rear+=1
        else:
            x = str(x)
            front = half_len -1
            rear = half_len + 1
            while rear < len(x):
                if x[front]!=x[rear]:
                    flag = 0
                    break
                front-=1
                rear+=1
        if flag == 1:
            return True
        else:
            return False
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

## 解答2

​	思考一下能不将整数转为字符串来解决这个问题吗？其实可以通过两种方式来判断，第一种就是直接把数字的回文数字求出来，然后比较是否相等即可，第二种比较巧妙的是只取后一半的序列，然后和前一半去比较，巧用取余和除法就可以实现。

```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        flag =x
        if x<0 or(x !=0 and x % 10==0):
            return False
        r = 0
        while x > 0:
            r = x % 10 + r*10
            x//=10
        return r == flag
```



```python
class Solution:
    def isPalindrome(self, x):
        """
        :type x: int
        :rtype: bool
        """
        if x<0 or(x !=0 and x % 10==0):
            return False
        r = 0
        while x > r:
            r = x % 10 + r*10
            x//=10
        return r == x or r//10 ==x
```

复杂度分析：

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$