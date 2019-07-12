## 380.Insert Delete GetRandom O(1)

### 题目描述

设计一个支持在平均 时间复杂度 O(1) 下，执行以下操作的数据结构。

+ insert(val)：当元素 val 不存在时，向集合中插入该项。
+ remove(val)：元素 val 存在时，从集合中移除该项。
+ getRandom：随机返回现有集合中的一项。每个元素应该有相同的概率被返回。

**示例 :**

```
// 初始化一个空的集合。
RandomizedSet randomSet = new RandomizedSet();

// 向集合中插入 1 。返回 true 表示 1 被成功地插入。
randomSet.insert(1);

// 返回 false ，表示集合中不存在 2 。
randomSet.remove(2);

// 向集合中插入 2 。返回 true 。集合现在包含 [1,2] 。
randomSet.insert(2);

// getRandom 应随机返回 1 或 2 。
randomSet.getRandom();

// 从集合中移除 1 ，返回 true 。集合现在包含 [2] 。
randomSet.remove(1);

// 2 已在集合中，所以返回 false 。
randomSet.insert(2);

// 由于 2 是集合中唯一的数字，getRandom 总是返回 2 。
randomSet.getRandom();
```



### 解答

​	如果只是用list来解决，插入是常数时间，但是remove的时候是需要查找的，所以不再是常数时间，所以这里需要用一个hashmap来记录num的位置，这样查找也是常数空间，只不过remove后需要改变两个数据结构的状态。

```python
class RandomizedSet:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        # list和hashmap
        self.l = []
        self.d = {}

    def insert(self, val: int) -> bool:
        """
        Inserts a value to the set. Returns true if the set did not already contain the specified element.
        """
        if val not in self.d:
            self.d[val] = len(self.l)
            self.l.append(val)
            return True
        return False

    def remove(self, val: int) -> bool:
        """
        Removes a value from the set. Returns true if the set contained the specified element.
        """
        if val in self.d:
            self.d[self.l[-1]] = self.d[val]
            self.l[self.d.pop(val)] = self.l[-1]
            self.l.pop()
            return True
        return False
    def getRandom(self) -> int:
        """
        Get a random element from the set.
        """
        if self.l:
            return self.l[random.randint(0,len(self.l)-1)]
        return 
        


# Your RandomizedSet object will be instantiated and called as such:
# obj = RandomizedSet()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```

