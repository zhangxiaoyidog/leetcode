## 207.Course Schedule

## 题目描述

现在你总共有 *n* 门课需要选，记为 `0` 到 `n-1`。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: `[0,1]`

给定课程总量以及它们的先决条件，判断是否可能完成所有课程的学习？

**示例 1:**

```
输入: 2, [[1,0]] 
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
```

**示例 2:**

```
输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。
```

**说明:**

1. 输入的先决条件是由**边缘列表**表示的图形，而不是邻接矩阵。详情请参见[图的表示法](http://blog.csdn.net/woaidapaopao/article/details/51732947)。
2. 你可以假定输入的先决条件中没有重复的边。

**提示:**

1. 这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
2. [通过 DFS 进行拓扑排序](https://www.coursera.org/specializations/algorithms) - 一个关于Coursera的精彩视频教程（21分钟），介绍拓扑排序的基本概念。
3. 拓扑排序也可以通过 [BFS](https://baike.baidu.com/item/%E5%AE%BD%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2/5224802?fr=aladdin&fromid=2148012&fromtitle=%E5%B9%BF%E5%BA%A6%E4%BC%98%E5%85%88%E6%90%9C%E7%B4%A2) 完成。



### 解答

​	这道题就相当于查找有向图是否存在拓扑排序，也就是每次把入度为0的节点删除，然后看最后是否剩下节点，如果不剩，那么就存在拓扑排序，否则不存在。

​	那么这道题就可以利用这个来解题，首先把每个节点的入度计算出来，然后定义一个队列，假如入度为0的节点，然后去出队里面的节点，找到这些节点指向的节点,并把这些节点的入度减去1，如这些节点入度变成0了，那就加入队列。

​	最后的判断也是很有技巧的，每次遍历一个入度为0的节点，就把numCourses减去1，最后需要判断numCourses是否大于0即可。

```python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: 'List[List[int]]') -> bool:
        # 判断一个图是否存在拓扑排序
        # b[]表示每个点的入度
        b = [0] * numCourses
        for prerequisite in prerequisites:
            b[prerequisite[1]] += 1
        # 定义一个队列，里面是入度为0的节点
        queues = []
        for i in range(len(b)):
            if b[i] == 0:
                queues.append(i)
        # 找到入度为0的节点指向的节点,并把这些节点的入度减去1
        while len(queues) != 0:
            numCourses -= 1
            this_node = queues.pop(0)
            for i in range(len(prerequisites)):
                if prerequisites[i][0] == this_node:
                    b[prerequisites[i][1]] -= 1
                    if b[prerequisites[i][1]] == 0:
                        queues.append(prerequisites[i][1])

        return False if numCourses > 0 else True
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$ 

