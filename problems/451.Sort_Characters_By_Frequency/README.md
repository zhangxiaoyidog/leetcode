## 451.Sort Characters By Frequency

## 题目描述

给定一个字符串，请将字符串里的字符按照出现的频率降序排列。

**示例 1:**

```
输入:
"tree"

输出:
"eert"

解释:
'e'出现两次，'r'和't'都只出现一次。
因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。
```


**示例 2:**

```
输入:
"cccaaa"

输出:
"cccaaa"

解释:
'c'和'a'都出现三次。此外，"aaaccc"也是有效的答案。
注意"cacaca"是不正确的，因为相同的字母必须放在一起。
```


示例 3:

```
输入:
"Aabb"

输出:
"bbAa"

解释:
此外，"bbaA"也是一个有效的答案，但"Aabb"是不正确的。
注意'A'和'a'被认为是两种不同的字符。
```



### 解答

​	这道题其实和347非常相似，我这里采用字典存储字母和对应出现个数，使用sorted函数排序后输出，假如不使用sorted函数应该用桶排序的思想，新建一个桶，将每个字符存入索引为它的频次的那个桶中。由于桶的索引本身就是自增的，因此这样就直接利用桶完成了对每个字符按照它的出现次数进行了从大到小的排序。倒着遍历桶，将每个桶里的元素取出来，并按照它的频次存入要返回的结果中。

```python
class Solution(object):
    def frequencySort(self, s):
        """
        :type s: str
        :rtype: str
        """
        d = {}
        for c in s:
            d[c] = d.get(c, 0) + 1
        # sorted函数时间复杂度应该是nlogn
        list1 = sorted(d.items(),key=lambda x:x[1],reverse=True)
        res = ''
        for item in list1:
            res+=item[0]*item[1]
        return res
```

