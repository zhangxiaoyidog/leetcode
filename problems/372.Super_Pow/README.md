## 372.Super Pow

### 题目描述

你的任务是计算 ab 对 1337 取模，a 是一个正整数，b 是一个非常大的正整数且会以数组形式给出。

**示例 1:**

```
输入: a = 2, b = [3]
输出: 8
```


**示例 2:**

```
输入: a = 2, b = [1,0]
输出: 1024
```



### 解答

​	这道题我是采用嵌套递归的方法来计算结果，比如计算2^26，可以把它分解成(2 ^2) ^10*2 ^6，并且2 ^6可以分解为(2 * 2)^3。

```python
class Solution:
    def superPow(self, a: int, b: List[int]) -> int:
        res = 1
        for x in b:
            res = self.pow(res,10)*self.pow(a,x)%1337
        return res
    def pow(self,a,b):
        if a==1 or b==0:
            return 1
        if b%2:
            return a*self.pow(a,b-1)%1337
        return self.pow(a*a%1337,b//2)%1337
```




