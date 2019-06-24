## 342.Power of Four

## 题目描述

给定一个整数 (32 位有符号整数)，请编写一个函数来判断它是否是 4 的幂次方。

**示例 1:**

```
输入: 16
输出: true
```

**示例 2:**

```
输入: 5
输出: false
```


进阶：
你能不使用循环或者递归来完成本题吗？



### 解答1

```python
class Solution(object):
    def isPowerOfFour(self, num):
        """
        :type num: int
        :rtype: bool
        """
        ini = 1
        while ini<num:
            ini*=4
        return ini==num
```



### 解答2

```python
import math
class Solution(object):
    def isPowerOfFour(self, num):
        """
        :type num: int
        :rtype: bool
        """
        
        return num>0 and math.log(num,4)==int(math.log(num,4))
```

​	在评论区还看到一种解答，理论上数字4幂的二进制类似于100，10000，1000000，etc...形式。可以有如下结论：4的幂一定是2的。4的幂和2的幂一样，只会出现一位1。但是，4的1总是出现在奇数位。`0x5 = 0101b`可以用来校验奇数位上的1。

```python
# 0b1010101010101010101010101010101
return num>0 and (num & num - 1)==0 and (num & 0x55555555)==num
```

