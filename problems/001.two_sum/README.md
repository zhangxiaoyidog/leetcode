# 001. Two Sum

## 题目描述

给定一个整数数组和一个目标值，找出数组中和为目标值的**两个**数。

你可以假设每个输入只对应一种答案，且同样的元素不能被重复利用。

**示例:**

```python
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

## 解答1

 	一开始最先想到的方法就是使用暴力法求解，即用两个for循环来遍历所有的解空间，直到找到结果返回。这样做虽然简单直接，但是代价是时间复杂度非常高。

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int size;
        size = nums.length;
        int[] a = new int[2];
        for(int i = 0;i<size;i++){
            for(int j = i+1;j<size;j++){
                if(nums[i]+nums[j] == target){
                    a[0] = i;
                    a[1] = j;
                    return a;
                }
        }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```

```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i] + nums[j] == target:
                    return [i,j]
```



>复杂度分析：
>
>+ 时间复杂度：$O(n^2)$
>
>+ 空间复杂度：$O(1)$

## 解答2

​	思考一下，我们需要对时间复杂度进行优化，一般是要以空间为代价来换取时间的，所以我们需要使用哈希表来帮助我们解决这个问题，建立一个hash表(python中的字典)来将nums中的值存为键，把对应的index存储为value，然后把原问题转化成减法，也就是在遍历的过程中去寻找target-nums[i]的值是否在hash表中，这样时间复杂度就降到了$O(n)$，但是空间复杂度升高。

```python
class Solution:
    def twoSum(self, nums, target):  
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        re_dict = {}
        for i ,num in enumerate(nums):
            if target - num in re_dict:
                return [re_dict[target - num],i]
            re_dict[num] = i       
```



>复杂度分析：
>
>+ 时间复杂度$O(n)$:遍历了一遍数组，查找的过程是$O(1)$
>+ 空间复杂度$O(n)$:建立了一个hash表，最大可能需要存储所有的元素

