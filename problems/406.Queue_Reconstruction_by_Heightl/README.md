## 406.Queue Reconstruction by Height

### 题目描述

假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对(h, k)表示，其中h是这个人的身高，k是排在这个人前面且身高大于或等于h的人数。 编写一个算法来重建这个队列。

**注意：**
总人数少于1100人。

**示例**

```
输入:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

输出:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```



### 解答

​	这道题比较有技巧性，首先要根据身高降序排序，然后遍历时候直接插入到k位置，因为后面插入的时候并不影响前面的，这里排序的时候也要考虑到k，因为比如[5,3]和[5,2]，假如排序的时候把[5,3]放到了[5,2]的前面，那么他们之间可能就还有其他的数字，这样就会出错，所以还有一个原则是要考虑k。

```python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        # 先根据身高降序,然后遍历往前插
        people.sort(key=lambda a:a[0],reverse=True)
        
        res = []
        for p in people:
            res.insert(p[1],p)
        return res
```
