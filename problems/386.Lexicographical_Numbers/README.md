## 386.Lexicographical Numbers

### 题目描述

给定一个整数 n, 返回从 1 到 n 的字典顺序。

例如，

给定 n =13，返回 [1,10,11,12,13,2,3,4,5,6,7,8,9] 。

请尽可能的优化算法的时间复杂度和空间复杂度。 输入的数据 n 小于等于 5,000,000。



### 解答1

1 10 100 1000 …… 100*01 100\*02　……　2 20 200……

```python
class Solution:
    def lexicalOrder(self, n: int) -> List[int]:
        # 直接使用排序函数
        # return [int(i) for i in sorted([str(i) for i in range(1,n+1)])]
        
        # 迭代的方法
        res = [0]*n
        num = 1
        for i in range(n):
            res[i] = num
            if num*10<=n:
                num*=10
            else:
                while num%10==9 or num==n:
                    num//=10
                num+=1
        return res
```



### 解答2

```python
class Solution:
    def lexicalOrder(self, n: int) -> List[int]:
        # 递归
        res = []
        
        def dfs(a,res):
            if a>n:
                return
            res.append(a)
            for i in range(10):
                dfs(a*10+i,res)
        for i in range(1,10):
            dfs(i,res)
        return res
            
```

