## 049.**Group Anagrams**

### 题目描述

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

**示例:**

```
输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
输出:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**说明：**

- 所有输入均为小写字母。
- 不考虑答案输出的顺序。



### 解答

这道题我是参考了网上的解题思路，大概的思想就是去遍历字符串数组，首先先将字符串排序，然后借助一个字典判断是否已有异位词，并且插入到待返回列表的合适的位置中。

```python
class Solution:
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        res = []
        base_dic = {}
        index = 0
        def sortstr(str_temp):
            sort_li = list(str_temp)
            sort_li.sort()
            return ''.join(sort_li)
        
        for str_one in strs:
            str_sort = sortstr(str_one)
            if str_sort in base_dic.keys():
                res[base_dic[str_sort]].append(str_one)
            else:
                base_dic[str_sort] = index
                res.append([str_one])
                index+=1
        return res
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)​$ 

