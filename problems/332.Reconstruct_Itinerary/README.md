## 332.Reconstruct Itinerary

## 题目描述

给定一个机票的字符串二维数组 [from, to]，子数组中的两个成员分别表示飞机出发和降落的机场地点，对该行程进行重新规划排序。所有这些机票都属于一个从JFK（肯尼迪国际机场）出发的先生，所以该行程必须从 JFK 出发。

**说明:**

1. 如果存在多种有效的行程，你可以按字符自然排序返回最小的行程组合。例如，行程 ["JFK", "LGA"] 与 ["JFK", "LGB"] 相比就更小，排序更靠前
2. 所有的机场都用三个大写字母表示（机场代码）。
3. 假定所有机票至少存在一种合理的行程。

**示例 1:**

```
输入: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
输出: ["JFK", "MUC", "LHR", "SFO", "SJC"]
```

**示例 2:**

```
输入: [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
输出: ["JFK","ATL","JFK","SFO","ATL","SFO"]
解释: 另一种有效的行程是 ["JFK","SFO","ATL","JFK","ATL","SFO"]。但是它自然排序更大更靠后。
```



### 解答

​	使用dfs求解，模板还是之前的形式，先把tickets做一个sort操作，这样就可以保证说明1中的问题可以解决，然后使用dfs寻找一个有向图的欧拉路径，这里需要注意一种情况就是找不到出口的情况，也就是`[["JFK","KUL"],["JFK","NRT"],["NRT","JFK"]]`走KUL这条路的这种情况，加一个判断条件即可。

```python
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        # dfs求解
        tickets.sort()
        use = [0] * (len(tickets)+1)
        def dfs(s,res):
            if len(res) == len(use):
                return res
            for i in range(len(tickets)):
                if use[i]==0 and s==tickets[i][0]:
                    use[i]=1
                    r =  dfs(tickets[i][1],res+[tickets[i][1]])
                    # 找不到出口
                    if not r:
                        use[i]=0
                    else:
                        return r
        return dfs('JFK',['JFK'])
```

