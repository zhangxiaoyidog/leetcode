## 126.Word Ladder II

## 题目描述

给定两个单词（*beginWord* 和 *endWord*）和一个字典 *wordList*，找出所有从 *beginWord* 到 *endWord* 的最短转换序列。转换需遵循如下规则：

1. 每次转换只能改变一个字母。
2. 转换过程中的中间单词必须是字典中的单词。

**说明:**

- 如果不存在这样的转换序列，返回一个空列表。
- 所有单词具有相同的长度。
- 所有单词只由小写字母组成。
- 字典中不存在重复的单词。
- 你可以假设 *beginWord* 和 *endWord* 是非空的，且二者不相同。

**示例 1:**

```
输入:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

输出:
[
  ["hit","hot","dot","dog","cog"],
  ["hit","hot","lot","log","cog"]
]
```

**示例 2:**

```
输入:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

输出: []

解释: endWord "cog" 不在字典中，所以不存在符合要求的转换序列。
```



### 解答

​	这道题是真的比较难，如果使用127题的方式，则只能得到一种结果，所以修改成DFS来解决问题，中间也遇到了很多问题，比如还是只能得到一种结果，是因为在获取neighbor的时候del了已经访问过的节点，假如不del，获取到的neghbor又会包括走过的节点，所以在这里参考了别人的一种方法。

​	首先使用BFS得到beginWord和其他节点的距离，在使用深度优先遍历的时候通过判断距离来判断是否已经走过，这个问题得以解决。但是时间复杂度和空间复杂度都比较高。

```python
# coding=utf-8

class Solution:
    def findLadders(self, beginWord: 'str', endWord: 'str', wordList: 'List[str]') -> 'List[List[str]]':
        """
        这道题如果用BFS，只能得到一种结果，所以修改成DFS
        """
        if endWord not in wordList:
            return []
        wordSet = {}
        for w in wordList:
            wordSet[w] = 1
        res = []
        temp_list = [beginWord]
        # 先bfs得到距离字典
        distance = self.bfs_distance(beginWord, wordSet)

        return self.dfs(beginWord, endWord, wordSet, temp_list, distance, res)

    def bfs_distance(self, beginWord, wordSet):
        """
        得到beginWord和其他节点的距离
        :return:
        """
        distance = {beginWord: 0}
        queue = []
        queue.append(beginWord)
        while queue:
            word = queue[0]
            queue.pop(0)

            nextWords = self.nextWordList(word, wordSet)
            for nextword in nextWords:
                if nextword not in distance:
                    distance[nextword] = distance[word] + 1
                    queue.append(nextword)
        return distance

    def dfs(self, beginWord, endWord, wordSet, temp_list, distance, res):
        """
        深度遍历得到所有的结果
        """

        if beginWord == endWord:
            res.append(list(temp_list))
        next_words = self.nextWordList(beginWord, wordSet)
        for next_word in next_words:
            if distance.get(next_word, -2) - 1 == distance[beginWord]:
                temp_list.append(next_word)
                self.dfs(next_word, endWord, wordSet, temp_list, distance, res)
                temp_list.remove(next_word)
        return res

    def nextWordList(self, word, wordSet):
        res_list = []
        all_lowers = 'abcdefghijklmnopqrstuvwxyz'
        for i in range(len(word)):
            for lower in all_lowers:
                new_word = list(word)
                if lower != new_word[i]:
                    new_word[i] = lower
                    new_word = ''.join(new_word)
                    if new_word in wordSet:
                        res_list.append(new_word)
        return res_list
```

