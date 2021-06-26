---
top: 0
title: 【Puzzle】Coin-in-Square
abbrlink: ecb676f8
date: 2021-06-02 10:03:57
tags:
  - 概率
  - Puzzle
categories:
  - 数
  - 概率
thumbnail: https://i.loli.net/2021/05/25/FXob8M72YK1nhLD.jpg
---

参考: 《Fifty challenging problems in probability with solutions》 

---

# 问题描述

>In a common carnival game a player tosses a penny from a distance of about 5 feet onto the surface of a table ruled in 1-inch squares
>
>If the penny (3/4 inch in diameter) falls entirely inside a square, the player receives 5 cents but does not get his penny back
>
>Otherwise, he loses the penny
>If the penny lands on the table, what is his chance to win?

在一个游戏中，一个玩家从5英尺远的地方把一分钱硬币扔到一张1英寸正方形的桌子上，硬币直径为 3/4 英寸。

如果硬币完全落在正方形内，则玩家赢。

如果硬币落在桌上，他赢的机会有多大？

# 思路参考

如果硬币可以落在桌子上，那么硬币的重心在正方形范围内。

![](https://i.loli.net/2021/06/02/eslvEXHFIMqbT4B.jpg)

如果硬币完全落在正方形内，硬币重心到正方形四条边的距离都要大于硬币的半径。

硬币半径为 3/8 英寸。设硬币重心为 (x, y)，那么要满足以上条件，需要

$$
\left\{
\begin{array}{**lr**}  
x >= 3/8 \\
y >= 3/8 \\
1 - x >= 3/8 \\
1 - y >= 3/8 \\
\end{array}  
\right.
$$

求出 (x, y) 的范围是 (3/8 ~ 5/8, 3/8 ~ 5/8)。

因此当硬币落在桌子上的条件下，赢的机会有 `(1/4 * 1/4) / 1 = 1/16 = 0.0625` 

# 蒙特卡洛模拟

```python
import numpy as np

def check(x, y):
    return x >= 3/8 and (1 - x) >= 3/8 and y >= 3/8 and (1 - y) >= 3/8

def test():
    T = int(1e7)
    s = 0
    for t in range(T):
        x = np.random.rand()
        y = np.random.rand()
        if check(x, y):
            s += 1
    print("his chance to win: {:.6f}".format(s / T))

for i in range(10):
    test()
```

模拟结果

```plain
his chance to win: 0.062507
his chance to win: 0.062518
his chance to win: 0.062433
his chance to win: 0.062596
his chance to win: 0.062261
his chance to win: 0.062555
his chance to win: 0.062552
his chance to win: 0.062652
his chance to win: 0.062406
his chance to win: 0.062344
```
