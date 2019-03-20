## 058.Length of Last Word

###题目描述

给定一个仅包含大小写字母和空格 `' '` 的字符串，返回其最后一个单词的长度。

如果不存在最后一个单词，请返回 0 。

**说明：**一个单词是指由字母组成，但不包含任何空格的字符串。

**示例:**

```
输入: "Hello World"
输出: 5
```



### 解答

​	这道题并不难，做法大概是先‘去除’字符串最后的空格。也就是找到从右往左第一个不为空格的位置，然后在从前往这个位置去遍历，一到空格就从新开始计数，返回最后的计数结果即可。

```python
class Solution:
    def lengthOfLastWord(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s) == 0:
            return 0
        cursor = len(s)
        while s[cursor-1] == ' ':
            cursor -= 1
            if cursor == 0:
                return 0
        count = 0
        for c in s[:cursor]:
            if c == ' ':
                count = 0
            else:
                count += 1
        return count
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 