## 211. Add and Search Word - Data structure design

## 题目描述

设计一个支持以下两种操作的数据结构：

```
void addWord(word)
bool search(word)
```

search(word) 可以搜索文字或正则表达式字符串，字符串只包含字母 `.` 或 `a-z` 。 `.` 可以表示任何一个字母。

**示例:**

```
addWord("bad")
addWord("dad")
addWord("mad")
search("pad") -> false
search("bad") -> true
search(".ad") -> true
search("b..") -> true
```

**说明:**

你可以假设所有单词都是由小写字母 `a-z` 组成的。



### 解答1

​	第一种比较容易想到的就是使用一个list去存储add进来的word，在search的时候就直接遍历所有的情况，但是提交超时。

```python
class WordDictionary:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.store = []

    def addWord(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        self.store.append(word)

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        """
        for candi in self.store:
            if len(candi) != len(word):
                continue
            flag = 1

            for char1, char2 in zip(candi, word):
                if char1 != char2 and char2 != '.':
                    flag = 0
                    break
            if flag == 1:
                return True
        return False
                    

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```



### 解答2

​	这里比较容易可以联想到使用208题的Trie树的解法，但是这里有'.'的这种情况我们需要使用dfs来做，所以在递归的过程中要判断两种情况，也就是当前字母是'.'的这种和其他的字母，如果是就可以匹配任意字符，可以分出很多路，如果不是则只有一条路。

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isWord = 0
        
        
class WordDictionary:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = TrieNode()

    def addWord(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        node = self.root
        for char in word:
            if char not in node.children:
                node.children[char] = TrieNode()
            node = node.children[char]
        node.isWord = 1
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        """
        def dfs_search(node,i):
            if i == len(word):
                return node.isWord
            
            # 这里分两种情况
            if word[i] == '.':
                # 可以匹配任意一个children
                for child in node.children.values():
                    if dfs_search(child, i+1):
                        return True
            else:
                if word[i] in node.children:
                    if dfs_search(node.children[word[i]], i+1):
                        return True
            return False
        node = self.root
        return dfs_search(node,0)

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
```

