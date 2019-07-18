## 401.Bibary Watch

### 题目描述

二进制手表顶部有 4 个 LED 代表小时（0-11），底部的 6 个 LED 代表分钟（0-59）。

每个 LED 代表一个 0 或 1，最低位在右侧。

![](https://upload.wikimedia.org/wikipedia/commons/8/8b/Binary_clock_samui_moon.jpg)

例如，上面的二进制手表读取 “3:25”。

给定一个非负整数 n 代表当前 LED 亮着的数量，返回所有可能的时间。

**案例:**

```
输入: n = 1
返回: ["1:00", "2:00", "4:00", "8:00", "0:01", "0:02", "0:04", "0:08", "0:16", "0:32"]
```



**注意事项:**

```
输出的顺序没有要求。
小时不会以零开头，比如 “01:00” 是不允许的，应为 “1:00”。
分钟必须由两位数组成，可能会以零开头，比如 “10:2” 是无效的，应为 “10:02”。
```



### 解答

​	这道题也就是穷举所有的时间，然后判断二进制1的个数是否等于亮灯的个数即可。

```python
class Solution:
    def readBinaryWatch(self, num: int) -> List[str]:
        # 穷举所有的时间
        if num>8:
            return []
        if num==0:
            return ['0:00']
        res = []
        bins = [str(bin(i))[2:].count('1') for i in range(60)]
        
        for hour in range(12):
            for minute in range(60):
                if bins[hour] + bins[minute] == num:
                    res.append('%d:%02d'%(hour, minute))
        return res
```

