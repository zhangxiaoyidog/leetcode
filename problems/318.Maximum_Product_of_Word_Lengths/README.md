## 318.Maximum Product of Word Lengths

## 题目描述

给定一个字符串数组 words，找到 length(word[i]) * length(word[j]) 的最大值，并且这两个单词不含有公共字母。你可以认为每个单词只包含小写字母。如果不存在这样的两个单词，返回 0。

**示例 1:**

```
输入: ["abcw","baz","foo","bar","xtfn","abcdef"]
输出: 16 
解释: 这两个单词为 "abcw", "xtfn"。
```


**示例 2:**

```
输入: ["a","ab","abc","d","cd","bcd","abcd"]
输出: 4 
解释: 这两个单词为 "ab", "cd"。
```

**示例 3:**

```
输入: ["a","aa","aaa","aaaa"]
输出: 0 
解释: 不存在这样的两个单词。
```



### 解答1

​	第一种就是使用暴力解答了，对每一对不同的word都去判断他们是否有公共字母，如果没有那么去判断当前res是否小于这两个word的长度乘积来更新res，最后返回res的值。但是时间超时orz

```python
class Solution:
    def maxProduct(self, words: List[str]) -> int:
        if len(words)<2:
            return 0
        res = 0
        for i in range(len(words)-1):
            for j in range(i+1,len(words)):
                if not self.judge(words[i],words[j]):
                    res = max(res,len(words[i])*len(words[j]))
            
        return res
                              
    def judge(self,word1,word2):
        # 判断两个word是否有公共字母
        for w1 in word1:
            for w2 in word2:
                if w1==w2:
                    return True
        return False
```

- 时间复杂度：$O(n^4)$
- 空间复杂度：$O(1)$ 



### 解答2

​	如何降低时间复杂度呢？那么就需要把judge这一步更改一下，这里可以使用set把words中的每一个word变成一个set，在判断的时候直接使用集合的与运算即可。

​	在网上还看到一种方法是差不多的思想，这里记录一下。具体是使用bitmap位图的思想，对每一个word构造一个位图，利用`current_char - 'a'`的值来判断当前字符是哪个字符，并利用该差值确定存储该字符的位置：

- `'a' - 'a' = 0`所以，a会放到第0位，对应的从右往左的移位数为0；
- `'b' - 'a' = 1`所以，b会放到第1位，对应的从右往左的移位数为1；
- ...
- `'z' - 'a' = 25`所以，z会放到第25位，对应的从右往左的移位数为25；

通过上面的观察，我们可以发现，利用 `bitmap |= (1 << (words.charAt(i) - 'a'))`可以实现单词变bitmap。最后再使用与运算去判断两个word是否有相同字符。

```python
class Solution:
    def maxProduct(self, words: List[str]) -> int:
        n = len(words)
        res = 0
        sets = [set(i) for i in words]
        for i in range(n):
            for j in range(i + 1, n):
                if not sets[i] & sets[j]:
                    res = max(res, len(words[i]) * len(words[j]))
        return res
```

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(n)$ 