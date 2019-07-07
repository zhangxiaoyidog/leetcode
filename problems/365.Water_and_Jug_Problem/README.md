## 367.Water and Jug Problem

### 题目描述

有两个容量分别为 x升 和 y升 的水壶以及无限多的水。请判断能否通过使用这两个水壶，从而可以得到恰好 z升 的水？

如果可以，最后请用以上水壶中的一或两个来盛放取得的 z升 水。

你允许：

+ 装满任意一个水壶
+ 清空任意一个水壶
+ 从一个水壶向另外一个水壶倒水，直到装满或者倒空

**示例 1: (From the famous "Die Hard" example)**

```
输入: x = 3, y = 5, z = 4
输出: True
```


**示例 2:**

```
输入: x = 2, y = 6, z = 5
输出: False
```



### 解答

数学中有个定理：

```
如果gcd(x,y) = k //gcd函数用以计算两个数的最大公约数greatest common divisor简写 
那么肯定有整数（正的或负的）m与n，使得 mx + ny = k
```

如果z % k == 0, 那么mx + ny = k那么必定存在一个常数g使得g(mx + ny) == k * g == z  所以题目就转换为寻找x，y的最大公约数。

```python
class Solution:
    def canMeasureWater(self, x: int, y: int, z: int) -> bool:
        if x+y<z:
            return False
        if x==z or y==z or x+y==z:
            return True
        return z%self.gcd(x,y)==0
    def gcd(self,x,y):
        # 辗转相除求最大公约数
        if x<y:
            x,y=y,x
        while y!=0:
            temp = y
            y = x%y
            x = temp
        return x
```

