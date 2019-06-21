## 336.Palindrome Pairs

## 题目描述

给定一组唯一的单词， 找出所有不同 的索引对(i, j)，使得列表中的两个单词， words[i] + words[j] ，可拼接成回文串。

**示例 1:**

```
输入: ["abcd","dcba","lls","s","sssll"]
输出: [[0,1],[1,0],[3,2],[2,4]] 
解释: 可拼接成的回文串为 ["dcbaabcd","abcddcba","slls","llssssll"]
```

**示例 2:**

```
输入: ["bat","tab","cat"]
输出: [[0,1],[1,0]] 
解释: 可拼接成的回文串为 ["battab","tabbat"]
```



### 解答1

​	对于每两个word，都判断能否拼接成回文串，但是提交超时。

```python
class Solution:
    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        res = []
        if len(words)<2:
            return res

        for i in range(len(words)-1):
            for j in range(i+1,len(words)):            
                if self.isPalindrome(words[i]+words[j]):
                    res.append([i,j])
                if self.isPalindrome(words[j]+words[i]):
                    res.append([j,i])
        return res
                    
    def isPalindrome(self, s):
        start = 0
        end = len(s)-1
        while start<end:
            if s[start]!=s[end]:
                return False
            start+=1
            end-=1
        return True
```



- 时间复杂度：$O(n^3)$
- 空间复杂度：$O(n)$ 



### 解答2

​	其实能组成回文串也就三种情况： 如果自己的翻转后的字符串也在数组里，可以组成一对，注意翻转后不能是自己。 如果某个字符串能找到一个分割点，分割点前的部分是回文，后半部分翻转后也在数组里，可组成一对。 如果某个字符串能找到一个分割点，前半部分翻转后也在数组里，分割点后的部分是回文，可组成一对。

​	所以可以对每一个word判断这三种情况，这里为什么可以减少时间复杂度呢，因为实际上并没有判断那么多次，如果有回文也不用判断那么长的字符串。可以说是利用了关键信息。

```python
class Solution:
    def palindromePairs(self, words: List[str]) -> List[List[int]]:
        res = []
        if len(words)<2:
            return res
        #将字符串作为键，下标为值构建字典
        word_dic = dict(zip(words,range(len(words))))
        for i in range(len(words)):
            word = words[i]
            for j in range(len(word)+1):
                # 前部分是回文
                if self.isPalindrome(word[:j]):
                    if word[j:][::-1] in word_dic and i!=word_dic[word[j:][::-1]]:
                        # 后半部分在列表里，翻转后不能等于自己,即j=0
                        res.append([word_dic[word[j:][::-1]],i])
            # print(res)
            for k in range(len(word)):
                # 后部分是回文,这里不用判断，因为不会出现空串的情况
                if self.isPalindrome(word[k:]):
                    print(word[k:],word_dic)
                    if word[:k][::-1] in word_dic:
                        # 前半部分在列表里
                        res.append([i,word_dic[word[:k][::-1]]])
                
        return res

    def isPalindrome(self, s):
        start = 0
        end = len(s)-1
        while start<end:
            if s[start]!=s[end]:
                return False
            start+=1
            end-=1
        return True
```

