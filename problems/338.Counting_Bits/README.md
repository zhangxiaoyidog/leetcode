## 338.Counting Bits

## 题目描述

给定一个非负整数 num。对于 0 ≤ i ≤ num 范围中的每个数字 i ，计算其二进制数中的 1 的数目并将它们作为数组返回。

**示例 1:**

```
输入: 2
输出: [0,1,1]
```

**示例 2:**

```
输入: 5
输出: [0,1,1,2,1,2]
```

**进阶:**

+ 给出时间复杂度为O(n*sizeof(integer))的解答非常容易。但你可以在线性时间O(n)内用一趟扫描做到吗？
+ 要求算法的空间复杂度为O(n)。
+ 你能进一步完善解法吗？要求在C++或任何其他语言中不使用任何内置函数（如 C++ 中的 __builtin_popcount）来执行此操作。



### 解答1

​	在遍历每一个数字的时，使用除以2取余的操作分别求得每个数作为二进制时1的数目。

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        res = [0]
        for i in range(1,num+1):
            res.append(self.count(i))
        return res
    
    def count(self,num):
        count = 0
        while num>0:
            if num%2==1:
                count+=1
            num>>=1
        return count
```

- 时间复杂度：$O(n*sizeof(integer))$
- 空间复杂度：$O(n)$ 



### 解答2

​	对于所有的数字只有两类，对于奇数，它肯定是比前面的偶数多一个1，对于偶数，它的最后一位肯定是0，所以它的1的个数肯定是和它除以2后的那个数所包含1的个数一样，也就是右移一位操作。

```
举例：
0=0  1=1 
2=10  3=11
6=110 7=111

2 = 10    4 = 100    8 = 1000
3 = 11    6 = 110    12 = 1100
```



```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        res = [0]
        for i in range(1,num+1):   
            if i%2==0:
                res.append(res[i//2])
            else:
                res.append(res[i-1]+1)
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

