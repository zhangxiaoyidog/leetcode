## 319.Bulb Switcher

## 题目描述

初始时有 n 个灯泡关闭。 第 1 轮，你打开所有的灯泡。 第 2 轮，每两个灯泡你关闭一次。 第 3 轮，每三个灯泡切换一次开关（如果关闭则开启，如果开启则关闭）。第 i 轮，每 i 个灯泡切换一次开关。 对于第 n 轮，你只切换最后一个灯泡的开关。 找出 n 轮后有多少个亮着的灯泡。

**示例:**

```
输入: 3
输出: 1 
解释: 
初始时, 灯泡状态 [关闭, 关闭, 关闭].
第一轮后, 灯泡状态 [开启, 开启, 开启].
第二轮后, 灯泡状态 [开启, 关闭, 开启].
第三轮后, 灯泡状态 [开启, 关闭, 关闭]. 
你应该返回 1，因为只有一个灯泡还亮着。
```



### 解答1

​	根据题目可以利用迭代的方式去循环模拟每一轮的灯泡状态，维护一个list，1表示开启，0表示关闭，最后返回list的和即可。但是超时了orz……

```python
class Solution:
    def bulbSwitch(self, n: int) -> int:
        init = [1]*n
        for i in range(1,n):
            for j in range(i,n,i+1):
                init[j] ^=1
        # print(init)
        return sum(init)
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 



### 解答2

思路: 举例: 1 代表开, 0 代表关

输入: 000000000

第一轮 : 111111111

第二轮 : 10 10 10 10 1

第三轮: 100 011 100

第四轮 : 1001 1111 0

第五轮 : 10010 1110

第六轮 : 100100 110

第七轮 : 1001000 10

第八轮 : 10010000 0

第九轮 : 100100001

结果: 3

**总结出来规律:** 

比如, 

对于第四个灯泡, 会切换开关的轮数是 第一轮, 第二轮, 第四轮, 以后就不会变, 

对于第九个灯泡, 会切换开关的轮数是 第一轮, 第三轮, 第九轮 以后就不会变

我们发现 : **能开方的数都会切换三次而处于亮的状态**

```python
class Solution:
    def bulbSwitch(self, n: int) -> int:
        return int(n**0.5)
```

- 时间复杂度：$O(1)$
- 空间复杂度：$O(n)$ 

