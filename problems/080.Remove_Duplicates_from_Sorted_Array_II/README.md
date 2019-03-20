## 080.Remove Duplicates from Sorted Array II

### 题目描述

给定一个排序数组，你需要在**原地**删除重复出现的元素，使得每个元素最多出现两次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在**原地修改输入数组**并在使用 O(1) 额外空间的条件下完成。

**示例 1:**

```
给定 nums = [1,1,1,2,2,3],

函数应返回新长度 length = 5, 并且原数组的前五个元素被修改为 1, 1, 2, 2, 3 。

你不需要考虑数组中超出新长度后面的元素。
```

**示例 2:**

```
给定 nums = [0,0,1,1,1,1,2,3,3],

函数应返回新长度 length = 7, 并且原数组的前五个元素被修改为 0, 0, 1, 1, 2, 3, 3 。

你不需要考虑数组中超出新长度后面的元素。
```

**说明:**

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以**“引用”**方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

```
// nums 是以“引用”方式传递的。也就是说，不对实参做任何拷贝
int len = removeDuplicates(nums);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中该长度范围内的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```



### 解答

​	这道题其实比较简单，首先列表长度小于3的情况是不用修改的，那就从2开始，使用一个游标指针来往前修改就行，但是这里有一个比较巧妙的地方就是，我们可以只用`nums[i]`和`nums[i-2]、nums[cursor-2]`比较，如果有一个不同的话，就可以直接修改。

```python
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)<3:
            return len(nums)
        cursor = 2
        for i in range(2,len(nums)):
            if nums[i] != nums[i-2] or nums[i]!=nums[cursor-2]:
                nums[cursor] = nums[i]
                cursor+=1
        return cursor
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(1)$ 