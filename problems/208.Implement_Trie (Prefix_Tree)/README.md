## 208.Implement Trie (Prefix Tree)

## 题目描述

实现一个 Trie (前缀树)，包含 `insert`, `search`, 和 `startsWith` 这三个操作。

**示例:**

```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```

**说明:**

- 你可以假设所有的输入都是由小写字母 `a-z` 构成的。
- 保证所有输入均为非空字符串。



### 解答

​	这道题需要使用数据结构来实现一个前缀树，这里不能被这个树给迷惑了，不一定非要定义node，在这里我们可以使用字典嵌套来实现前缀树，对于每一个单词的每一个字母创建一个字典，假如之前有就往内一层，char是一个字典的key，它的值是以它为前缀的下一个字母，这样在search的时候只需要往内层去找就行了。

```python
class Trie:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.trie = {}

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self.trie
        for char in word:
            node = node.setdefault(char,{})
        node['end'] = True

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self.trie
        for char in word:
            if char not in node:
                return False
            node = node[char]
        if 'end' in node:
            return True
        return False

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self.trie
        for char in prefix:
            if char not in node:
                return False
            node = node[char]
        return True


# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

