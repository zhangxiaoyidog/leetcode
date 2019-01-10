## 093.Restore IP Addresses

## 题目描述

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

**示例:**

```
输入: "25525511135"
输出: ["255.255.11.135", "255.255.111.35"]
```



### 解答

​	这道题一看就知道是要用回溯法去解答，但是具体怎么解答并不知道，这一类题目到目前为止还是总结的比较少，所以看了网上的解答才知道，其实只要看到所有的组合，一般都是使用回溯，解这类题目的关键和难点是剪枝！！！还是要多加练习这类题目。

​	首先当然要判断s的长度是否大于12，大于12则直接返回，然后进入我们的　`dfs_ipaddress()`方法，其实还是我们之前说过的那个DFS模板的套路，path中存的就是ip的各段，一般这个方法的开始肯定是先定义出口，这里出口肯定是s为空并且path有4段。接着再去递归，使用一个for循环，这里解释一下为什么是`range(1, 4)`，是因为每一段最多有３个数字，这里还要判断001前面有0的这种情况，详细看代码即可知道算法流程，后来看到了题目中有别的同学的剪枝方法特别好，那就是每次dfs的时候都去检查一下所有的字符串的长度是不是能满足在最多4个3位数字组成，果然速度提升了很多

```python
class Solution:
    def restoreIpAddresses(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        res = []
        if len(s) > 12:
            return res

        self.dfs_ipaddress(res, s, [])
        return res

    def dfs_ipaddress(self, res, s, path):
        
        if len(s) < 4 - len(path) or len(s) > (4 - len(path))*3 :
            return
        if not s and len(path) == 4:
            res.append('.'.join(path))
            return

        for i in range(1, 4):
            if i > len(s):
                continue
            number = int(s[:i])

            if str(number) == s[:i] and number <= 255:
                self.dfs_ipaddress(res, s[i:], path + [s[:i]])

```

