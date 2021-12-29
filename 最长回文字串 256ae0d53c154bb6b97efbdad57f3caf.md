# 最长回文字串

知识点Key: 回文
解题方法Methods: 动态规划DP
难度Level: 简单Easy

给定一个字符串s, 找到s中最长的回文 子串 。

分析：

两种回文子串：单数长度，双数长度。

对于一个回文子串而言，如果长度大于2，那么将他首尾的两个字母去除之后，它仍然是一个回文子串。

根据这样的思路我们可以用动态规划的方法解决本题，我们用 dp[ i , j ]表示字符串 S 的第 i 到 j 个字母组成的串是回文串。

dp[ i , j ]：

- True， 如果子串 Si 到 Sj 是回文串
- False， 如果 Si 到 Sj 不是回文串，或者 S[ i , j ]本身不合法

那么就可以写出动态规划的转移方程：

 dp[ i , j ] = dp[ i+1 , j-1 ] AND Si == Sj

意思是，需要中间是回文子串，两头的两个字符相等，才能保证还是回文子串。

以上是对于长度 > 2 的子串，我们还需要考虑动态规划中的边界条件，即子串长度是 1 或者 2 的情况，分别是：

- dp[ i , j ] = True
- dp[ i , i+1 ] = Si == Si+1

这样所有 dp[ i , j ]为 True 的格子的 j-i+1 的最大值就是最长回文子串

代码：

```python
while True:
    try:
        s = str(input())
        n = len(s)
        if n < 2:
            print(s)
            continue
        max_len = 1
        begin = 0
        dp = [[False for x in range(n)] for y in range(n)]
        #创建dp
        for i in range(n):
            #边界条件，最基本的单个字母都是回文子串
            dp[i][i] = True
        # generating table
        for substringLength in range(2, n+1):
            for i in range(n-1):
                j = int(substringLength + i -1)
                if j >= n:
                    continue                   
                if s[i] == s[j]:

                    if j - i < 3:
                        dp[i][j] = True

                    else:
                        dp[i][j] = dp[i+1][j-1]
                if dp[i][j] and j - i +1 > max_len:
                    max_len = j - i + 1
                    begin = i
        print(len(s[begin : begin+ max_len]))
                
    except:
        break
```