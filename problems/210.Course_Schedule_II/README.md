## 210.Course Schedule II

## 题目描述

现在你总共有 *n* 门课需要选，记为 `0` 到 `n-1`。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: `[0,1]`

给定课程总量以及它们的先决条件，返回你为了学完所有课程所安排的学习顺序。

可能会有多个正确的顺序，你只要返回一种就可以了。如果不可能完成所有课程，返回一个空数组。

**示例 1:**

```
输入: 2, [[1,0]] 
输出: [0,1]
解释: 总共有 2 门课程。要学习课程 1，你需要先完成课程 0。因此，正确的课程顺序为 [0,1] 。
```

**示例 2:**

```
输入: 4, [[1,0],[2,0],[3,1],[3,2]]
输出: [0,1,2,3] or [0,2,1,3]
解释: 总共有 4 门课程。要学习课程 3，你应该先完成课程 1 和课程 2。并且课程 1 和课程 2 都应该排在课程 0 之后。
     因此，一个正确的课程顺序是 [0,1,2,3] 。另一个正确的排序是 [0,2,1,3] 。
```

**说明:**

1. 输入的先决条件是由**边缘列表**表示的图形，而不是邻接矩阵。详情请参见[图的表示法](http://blog.csdn.net/woaidapaopao/article/details/51732947)。
2. 你可以假定输入的先决条件中没有重复的边。

**提示:**

1. 这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
2. [通过 DFS 进行拓扑排序](https://www.coursera.org/specializations/algorithms) - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。
3. 拓扑排序也可以通过 [BFS](https://baike.baidu.com/item/%E5%AE%BD%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2/5224802?fr=aladdin&fromid=2148012&fromtitle=%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2) 完成。



### 解答

​	这道题用之前的方法也能做，这里用另一种方式，首先定义两个字典，别表示修读这门课需要预修的和这门课修过之后可以去学的，然后找出一开始入度为0的节点加入到res和需要学习的列表中，把这些节点一个个弹出的同时得到学习了他们之后可以学习的课程，判断这些课程现在是否可以学习，也就是先提条件是否都满足，若满足则加入。

```python
class Solution:
    def findOrder(self, numCourses: int, prerequisites: List[List[int]]) -> List[int]:
        # 分别表示修读这门课需要预修的和这门课修过之后可以去学的
        pre = collections.defaultdict(list)
        nexts = collections.defaultdict(list)
        
        for item in prerequisites:
            pre[item[0]].append(item[1]) 
            nexts[item[1]].append(item[0]) 
        
        to_learn = []
        res = []
        for i in range(numCourses):
            # 学习这门课前不需要学习任何一门课(入度为0)
            if i not in pre.keys():
                to_learn.append(i)
                res.append(i)
        finished = [0] * numCourses
        while len(to_learn)!=0:
            cur = to_learn.pop(0)
            finished[cur] = 1
            for course in nexts[cur]:
                flag = 1
                for need in pre[course]:
                    if finished[need]==0:
                        flag = 0
                if flag==1:
                    to_learn.append(course)
                    res.append(course)
        if sum(finished)==numCourses:
            return res
        return []
            
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 