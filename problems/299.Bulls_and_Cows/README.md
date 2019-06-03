## 299.Bulls and Cows

## 题目描述

你正在和你的朋友玩 [猜数字（Bulls and Cows）](https://baike.baidu.com/item/%E7%8C%9C%E6%95%B0%E5%AD%97/83200?fromtitle=Bulls+and+Cows&fromid=12003488&fr=aladdin)游戏：你写下一个数字让你的朋友猜。每次他猜测后，你给他一个提示，告诉他有多少位数字和确切位置都猜对了（称为“Bulls”, 公牛），有多少位数字猜对了但是位置不对（称为“Cows”, 奶牛）。你的朋友将会根据提示继续猜，直到猜出秘密数字。

请写出一个根据秘密数字和朋友的猜测数返回提示的函数，用 `A` 表示公牛，用 `B` 表示奶牛。

请注意秘密数字和朋友的猜测数都可能含有重复数字。

**示例 1:**

```
输入: secret = "1807", guess = "7810"

输出: "1A3B"

解释: 1 公牛和 3 奶牛。公牛是 8，奶牛是 0, 1 和 7。
```

**示例 2:**

```
输入: secret = "1123", guess = "0111"

输出: "1A1B"

解释: 朋友猜测数中的第一个 1 是公牛，第二个或第三个 1 可被视为奶牛。
```

**说明:** 你可以假设秘密数字和朋友的猜测数都只包含数字，并且它们的长度永远相等。



### 解答

​	一开始我是直接去判断两种情况，也就是对应位置是否相等和假如不相等的话，guess[i]是否在secret中，但是这样会有一个问题就是假如这个元素是之前对应位置相等的元素，那么Cows的数量就会增多而错误，例如1123和0111正确答案应该是1A1B，但是这样判断出来是1A3B。

​	所以正确的解法是使用两个dict，去存储两个字符串中对应位置不相等的这些元素的个数，最后再统计cows的数量就很方便了。

```python
class Solution:
    def getHint(self, secret: str, guess: str) -> str:
        bulls = 0
        cows = 0
        se = {}
        gu = {}
        for i in range(len(secret)):
            if secret[i]==guess[i]:
                bulls += 1
            else:
                if secret[i] in se:
                    se[secret[i]]+=1
                else:
                    se[secret[i]]=1
                    
                if guess[i] in gu:
                    gu[guess[i]]+=1
                else:
                    gu[guess[i]]=1
        for key in gu:
            if key in se:
                cows += min(gu[key],se[key])
        return str(bulls)+'A'+str(cows)+'B'         
```

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$​ 