## 393.UTF-8 Validation

### 题目描述

UTF-8 中的一个字符可能的长度为 1 到 4 字节，遵循以下的规则：

对于 1 字节的字符，字节的第一位设为0，后面7位为这个符号的unicode码。
对于 n 字节的字符 (n > 1)，第一个字节的前 n 位都设为1，第 n+1 位设为0，后面字节的前两位一律设为10。剩下的没有提及的二进制位，全部为这个符号的unicode码。
这是 UTF-8 编码的工作方式：

```
   Char. number range  |        UTF-8 octet sequence
      (hexadecimal)    |              (binary)
   --------------------+---------------------------------------------
   0000 0000-0000 007F | 0xxxxxxx
   0000 0080-0000 07FF | 110xxxxx 10xxxxxx
   0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
   0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```




给定一个表示数据的整数数组，返回它是否为有效的 utf-8 编码。

**注意:**
输入是整数数组。只有每个整数的最低 8 个有效位用来存储数据。这意味着每个整数只表示 1 字节的数据。

**示例 1:**

```
data = [197, 130, 1], 表示 8 位的序列: 11000101 10000010 00000001.
返回 true 。
这是有效的 utf-8 编码，为一个2字节字符，跟着一个1字节字符。
```

**示例 2:**

```
data = [235, 140, 4], 表示 8 位的序列: 11101011 10001100 00000100.
返回 false 。
前 3 位都是 1 ，第 4 位为 0 表示它是一个3字节字符。
下一个字节是开头为 10 的延续字节，这是正确的。
但第二个延续字节不以 10 开头，所以是不符合规则的。
```



### 解答

​	由于最大就只有四个字节，那么最笨的方法就是一种一种去判断。

```python
class Solution:
    def validUtf8(self, data: List[int]) -> bool:
        i = 0
        n = len(data)
        # 最大只有四个字节,就一种一种判断
        while i<n:
            # 一字节
            if 0<=data[i]<128:
                i+=1
            elif i+1<n and 192<=data[i]<224 and 128<=data[i+1]<192:
                i+=2
            elif i+2<n  and 224<=data[i]<240 and 128<=data[i+1]<192 and 128<=data[i+2]<192:
                i+=3
            elif i+3<n  and 240<=data[i]<248 and 128<=data[i+1]<192 and 128<=data[i+2]<192 and 128<=data[i+3]<192:
                i+=4
            else:
                return False
        return True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 



### 解答2

​	使用位运算去判断字节的个数和后面是否合法，首先我们创建了一个掩码，其值为10000000。接下来会用这个掩码和整数做 逻辑与 操作，这样就可以知道有多少个 1 了。（记住，整数可能非常大，但我们只需要处理前 8 比特），检查前两个比特是不是 10，我们可以用10000000和1000000。

```python
class Solution:
    def validUtf8(self, data: List[int]) -> bool:
        flag = 0
        mask1 = 1 << 7
        mask2 = 1 << 6
        for i in range(len(data)):
            # 处理开头
            if flag == 0:
                mask = 1 << 7
                while mask & data[i] != 0:
                    flag += 1
                    mask >>= 1
                if flag == 0:
                    continue
                if flag > 4 or flag == 1:
                    return False
            else:
                if not (mask1 & data[i] != 0 and mask2 & data[i] == 0):
                    return False
            flag -= 1
        return flag == 0
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 

