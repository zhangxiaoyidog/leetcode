## 433.Minimum Genetic Mutation

## 题目描述

一条基因序列由一个带有8个字符的字符串表示，其中每个字符都属于 "A", "C", "G", "T"中的任意一个。

假设我们要调查一个基因序列的变化。一次基因变化意味着这个基因序列中的一个字符发生了变化。

例如，基因序列由"AACCGGTT" 变化至 "AACCGGTA" 即发生了一次基因变化。

与此同时，每一次基因变化的结果，都需要是一个合法的基因串，即该结果属于一个基因库。

现在给定3个参数 — start, end, bank，分别代表起始基因序列，目标基因序列及基因库，请找出能够使起始基因序列变化为目标基因序列所需的最少变化次数。如果无法实现目标变化，请返回 -1。

**注意:**

1. 起始基因序列默认是合法的，但是它并不一定会出现在基因库中。
2. 所有的目标基因序列必须是合法的。
3. 假定起始基因序列与目标基因序列是不一样的。

**示例 1:**

```
start: "AACCGGTT"
end:   "AACCGGTA"
bank: ["AACCGGTA"]

返回值: 1
```


*示例 2:**

```
start: "AACCGGTT"
end:   "AAACGGTA"
bank: ["AACCGGTA", "AACCGCTA", "AAACGGTA"]

返回值: 2
```


**示例 3:**

```
start: "AAAAACCC"
end:   "AACCCCCC"
bank: ["AAAACCCC", "AAACCCCC", "AACCCCCC"]

返回值: 3
```



### 解答

​	这道题和[127](https://github.com/zhangxiaoyidog/leetcode/blob/master/problems/127.Word_Ladder/README.md)很相似，代码直接套进去就完事了，还是使用bfs转化成图的问题来做。

```python
class Solution:
    def minMutation(self, start: str, end: str, bank: 'List[str]') -> int:
        if end not in bank:
            return -1
        if start in bank:
            bank.remove(start)

        dic = {}
        for b in bank:
            dic[b] = 1
        return self.bfs(start, end, dic)

    def bfs(self, start, end, dic):
        queue = []
        queue.append([start, 0])
        while queue:
            word, step = queue[0][0], queue[0][1]
            queue.pop(0)
            if word == end:
                return step
            nextWords = self.next_series(word, dic)
            for nextword in nextWords:
                queue.append([nextword, step + 1])
        return -1

    def next_series(self, start, bank):
        res_list = []
        all_char = 'ACGT'
        for i in range(len(start)):
            for c in all_char:
                new_s = list(start)
                if c != new_s[i]:
                    new_s[i] = c
                    new_s = ''.join(new_s)
                    if new_s in bank:
                        res_list.append(new_s)
                        del bank[new_s]
        return res_list
```

