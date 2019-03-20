## 127.Word Ladder

## 题目描述

给定两个单词（*beginWord* 和 *endWord*）和一个字典，找到从 *beginWord* 到 *endWord* 的最短转换序列的长度。转换需遵循如下规则：

1. 每次转换只能改变一个字母。
2. 转换过程中的中间单词必须是字典中的单词。

**说明:**

- 如果不存在这样的转换序列，返回 0。
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

输出: 5

解释: 一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog",
     返回它的长度 5。
```

**示例 2:**

```
输入:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

输出: 0

解释: endWord "cog" 不在字典中，所以无法进行转换。
```



### 解答

​	这道题是比较难的，一开始想了很久都没做出来，想想还是对BFS的这一类题目不太熟悉吧，这道题需要转化成图的问题，把每一个单词看成图的一个节点，假如两个单词只有一个字母不同，那么它们即是相邻节点，那么这道题我们就转化成求某个节点到另一个节点的最短路径的问题，看到图的问题，就必须想到能不能使用BFS，也就是广度优先遍历来完成，这道题是可以的。

​	具体怎么做呢，首先如何让找到一个词周围的词呢？我们可以采取穷举的方式，遍历这个词的每个字母，然后替换成别的字母，看替换后形成的新词是否在wordList中，是的！这个题是走迷宫问题的变形！也就是说，我们每次变化有26个方向，如果变化之后的位置在wordList中，我们认为这个走法是合规的，那么我们就可以采用BFS啦，一层层遍历出去，看最后到达endWord的step是多少，当然这是在wordList包含endWord的基础上。

​	一开始我使用list去做wordList的去重操作，然后遍历会超时，使用字典，降低查找的复杂度。

```python

class Solution:
    def ladderLength(self, beginWord: 'str', endWord: 'str', wordList: 'List[str]') -> 'int':
        if endWord not in wordList:
            return 0 
        if beginWord in wordList:
            wordList.remove(beginWord)
        # 使用list超时，改用字典AC
        # wordset = list(set(wordList))
        # print(wordset)
        wordDict = {}
        for w in wordList:
            wordDict[w] = 1
        return self.bfs(beginWord,endWord,wordDict)
    
    def bfs(self,beginWord,endWord,wordset):
        """
        广度优先搜索最短路径
        """
        queue = []
        queue.append([beginWord,1])
        while queue:
            word, step = queue[0][0], queue[0][1]
            queue.pop(0)
            if word == endWord:
                return step
            nextWords = self.nextWordList(word,wordset)
            for nextword in nextWords:
                queue.append([nextword,step+1])
        return 0
    
    def nextWordList(self,word,wordset):
        """
        找到周围的词，也就是找出wordList中只有一个字母与当前点不一样的词
        """
        res_list = []
        all_lowers = 'abcdefghijklmnopqrstuvwxyz'
        for i in range(len(word)):
            for lower in all_lowers:
                new_word = list(word)
                if lower != new_word[i]:
                    new_word[i] = lower
                    new_word = ''.join(new_word)
                    if new_word in wordset:
                        res_list.append(new_word)
                        del wordset[new_word]
        return res_list 
```

