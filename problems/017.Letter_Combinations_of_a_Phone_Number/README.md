## 017.Letter Combinations of a Phone Number

### 题目描述

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**示例:**

```
输入："23"
输出：["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**说明:**
尽管上面的答案是按字典序排列的，但是你可以任意选择答案输出的顺序。

### 解答1

​	首先我想到的就是一个数字一个数字去迭代，用两个for循环来控制，第一个循环控制digits数字，第二个for循环来控制当前数字可能能产生的字符串的结果，最后输出结果。

```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        result = []
        nums_map = {
            '2': 'abc', '3': 'def', '4': 'ghi',
            '5': 'jkl','6': 'mno', '7': 'pqrs',
            '8': 'tuv', '9': 'wxyz'
        }
        if len(digits) == 0:
            return result
        result = [c for c in nums_map[digits[0]]]
        if len(digits) == 1:
            return result

        for i in range(1, len(digits)):
            re_strs = []
            for c in result:
                re_strs.extend([c + j for j in nums_map[digits[i]]])
            result = re_strs
        return result
```

复杂度分析：

- 时间复杂度：$O(n*3^n)$
- 空间复杂度：$O(3^n)$ 

### 解答2

​	这道题在写出上面的答案之后，我意识到其实可以用递归的思想去做，大概思路是不断递归digits[1:]取求解它的可能的组合，返回结果和第一个字母去组合生成最终的结果。

```python
class Solution:
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        result = []
        nums_map = {
            '2': 'abc', '3': 'def', '4': 'ghi',
            '5': 'jkl','6': 'mno', '7': 'pqrs',
            '8': 'tuv', '9': 'wxyz'
        }
        if len(digits) == 0:
            return result
        if len(digits) == 1:
            return [c for c in nums_map[digits[0]]]
        
        re_str = self.letterCombinations(digits[1:])
        for c in nums_map[digits[0]]:
            for j in re_str:
                result.append(c+j)
        return result
```

