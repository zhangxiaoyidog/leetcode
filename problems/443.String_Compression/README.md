## 443.String Compression

## 题目描述

给定一组字符，使用原地算法将其压缩。

压缩后的长度必须始终小于或等于原数组长度。

数组的每个元素应该是长度为1 的字符（不是 int 整数类型）。

在完成原地修改输入数组后，返回数组的新长度。

 

**进阶：**
你能否仅使用O(1) 空间解决问题？

 

**示例 1：*

```
输入：
["a","a","b","b","c","c","c"]

输出：
返回6，输入数组的前6个字符应该是：["a","2","b","2","c","3"]

说明：
"aa"被"a2"替代。"bb"被"b2"替代。"ccc"被"c3"替代。
```

**示例 2：**

```
输入：
["a"]

输出：
返回1，输入数组的前1个字符应该是：["a"]

说明：
没有任何字符串被替代。
```

**示例 3：**

```
输入：
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

输出：
返回4，输入数组的前4个字符应该是：["a","b","1","2"]。

说明：
由于字符"a"不重复，所以不会被压缩。"bbbbbbbbbbbb"被“b12”替代。
注意每个数字在数组中都有它自己的位置。
```


**注意：**

1. 所有字符都有一个ASCII值在[35, 126]区间内。
2. 1 <= len(chars) <= 1000。



### 解答

​	最简单的方法是使用另一个list来存储第一次出现的字符，但是其实不用，我们直接在原数组上修改就好了。我的代码有些冗余，在disscuss中看到一个比较简洁的，这里也记录下来。

```python
class Solution:
    def compress(self, chars: 'List[str]') -> int:
        # 往前遍历的哨兵
        guard = 1
        start = 0
        this_char = 0
        count = 1

        while guard < len(chars):
            if chars[guard] == chars[this_char]:
                count += 1
            else:
                if count > 1:
                    for n in str(count):
                        chars[start + 1] = n
                        start += 1
                    count = 1
                    this_char = guard
                    start += 1
                else:
                    this_char = guard
                    start += 1

                if start < len(chars):
                    chars[start] = chars[this_char]
            guard += 1
        # 处理最后的字母
        if count > 1:
            for n in str(count):
                chars[start + 1] = n
                start += 1
        return start + 1
```



```python
class Solution:
    def compress(self, chars: 'List[str]') -> int:
        # 从后往前
        count = 1
        for i in range(len(chars)-1,-1,-1):
            if i>0 and chars[i]==chars[i-1]:
                count+=1
            else:
                end = i+count
                chars[i:end] = [chars[i]] if count==1 else [chars[i]]+list(str(count))
                count=1
        return len(chars)
```

