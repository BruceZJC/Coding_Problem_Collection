# 放苹果

知识点: 苹果分盘
解题方法: 递归
难度: 简单

题目描述

把m个同样的苹果放在n个同样的盘子里，允许有的盘子空着不放，问共有多少种不同的分法？（用K表示）5，1，1和1，5，1 是同一种分法。

数据范围：0<=m<=10，1<=n<=10。

输入两个int整数

分析：

递归思想

Base Case:

没有盘子/没有苹果/总共一个盘子一个苹果

放苹果有两种情况：

1. 有一个盘子为空，则问题缩减成 m 个苹果放入 n-1 个盘子里
2. 所有盘子都放上苹果，则还剩 m-n 个苹果，将被分配到 n 个盘子里

代码：

import sys
def distribution(m,n):
if m <0 or n < 0:
return 0
elif m == 1 or n == 1:
return 1
else:
return distribution(m, n-1) + distribution(m-n, n)

for i in sys.stdin.readlines():
m,n = i.split(' ')
print(distribution(int(m), int(n)))