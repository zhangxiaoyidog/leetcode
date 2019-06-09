## 310.Minimum Height Trees

## 题目描述

于一个具有树特征的无向图，我们可选择任何一个节点作为根。图因此可以成为树，在所有可能的树中，具有最小高度的树被称为最小高度树。给出这样的一个图，写出一个函数找到所有的最小高度树并返回他们的根节点。

格式

该图包含 n 个节点，标记为 0 到 n - 1。给定数字 n 和一个无向边 edges 列表（每一个边都是一对标签）。

你可以假设没有重复的边会出现在 edges 中。由于所有的边都是无向边， [0, 1]和 [1, 0] 是相同的，因此不会同时出现在 edges 里。

示例 1:

输入: n = 4, edges = [[1, 0], [1, 2], [1, 3]]

        0
        |
        1
       / \
      2   3 

输出: [1]
示例 2:

输入: n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

     0  1  2
      \ | /
        3
        |
        4
        |
        5 

输出: [3, 4]

说明:

+ 根据树的定义，树是一个无向图，其中任何两个顶点只通过一条路径连接。 换句话说，一个任何没有简单环路的连通图都是一棵树。
+ 树的高度是指根节点和叶子节点之间最长向下路径上边的数量。



### 解答

​	这道题要求把图转化成最小高度树后的root节点，由于图是无向的，所以任意选取一个点作为root节点即可生成一棵树，但是要如何生成一个最小高度树呢？可以直观地去想，如果可以取到最中间那一层的节点作为root，那肯定是最小高度树了，如何找呢，这里要使用剪枝的方法，也就是每一轮去删除那些度为1的节点，也就是叶子节点，这样就会慢慢往中间去找，最后只剩一个或者两个节点即为所求。

```python
class Solution:
    def findMinHeightTrees(self, n: int, edges: List[List[int]]) -> List[int]:
        if len(edges)==0:
            return [] if n==0 else [0]
        graph = {}
        for edge in edges:
            a,b = edge
            graph[a] = graph.get(a,[])+[b]
            graph[b] = graph.get(b,[])+[a]
        print(graph)
        while len(graph)>2:
            # 减掉叶节点
            leafs = [node for node in graph if len(graph[node])==1]
            parents = [graph[node][0] for node in leafs]

            for i, j in zip(leafs,parents):
                graph[j].remove(i)
            for i in leafs:
                del graph[i]

        return list(graph.keys())
```

