## 216.Combination Sum III

## 题目描述

找出所有相加之和为 **n** 的 **k** 个数的组合**。**组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

**说明：**

- 所有数字都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
```

**示例 2:**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
```

### 解答

​	这道题还是采取之前的做法，利用递归来解题，只不过这里的出口条件和进入条件需要修改一下而已，出口要加上一个当前集合的长度为3，进入的条件改为当前集合的长度小于3才行，这样跟之前的任务就一样了。

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        # 这个题用递归来解答
        self.res = []
        candicate = [1,2,3,4,5,6,7,8,9]
        self.dfs_search(candicate,n,0,[],k)
        return self.res
    
    def dfs_search(self,candicate,target,start,values,k):
        if target==0 and len(values)==k:
            return self.res.append(values)
        if len(values)<k:
            for i in range(start,len(candicate)):
                if candicate[i]>target:
                    return 
                self.dfs_search(candicate,target-candicate[i],i+1,values+[candicate[i]],k)
        
```

