## 038.**Count and Say**

### 题目描述

报数序列是一个整数序列，按照其中的整数的顺序进行报数，得到下一个数。其前五项如下：

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` 被读作  `"one 1"`  (`"一个一"`) , 即 `11`。
`11` 被读作 `"two 1s"` (`"两个一"`）, 即 `21`。
`21` 被读作 `"one 2"`,  "`one 1"` （`"一个二"` ,  `"一个一"`) , 即 `1211`。

给定一个正整数 *n*（1 ≤ *n* ≤ 30），输出报数序列的第 *n* 项。

注意：整数顺序将表示为一个字符串。

 

**示例 1:**

```
输入: 1
输出: "1"
```

**示例 2:**

```
输入: 4
输出: "1211"
```

### 解答

​	这道题关键在于理解题意，第一个数字为1，然后后面的每一个数字都是在解释前一个数字，所以第二个数字就是11（表示第一个数字为1个1），第三个数字为21（表示第二个数字为2个1），第四个数字为1211（表示第二个数字为1个2加1个1）……

​	理清楚逻辑后，采用简单的循环即可解题。

```python
class Solution:
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        if n==1:
            return '1'
        pre = '1'
        for i in range(2,n+1):
            re_str = ''
            count = 1
            for j in range(1,len(pre)):

                if pre[j] == pre[j-1]:
                    count+=1
                else:
                    re_str+= str(count)+pre[j-1]
                    count=1
            re_str+=str(count)+pre[-1]
            pre = re_str
        return re_str
                
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

