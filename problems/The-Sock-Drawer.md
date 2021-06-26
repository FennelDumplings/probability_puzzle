
# 写在前面

本题来自 《Fifty challenging problems in probability with solutions》。

---

# 问题描述

>The-Sock-Drawer
>-
>A drawer contains red socks and black socks
>When two socks are drawn at random, the probability that both are red is 1/2
>
>a. How small can the number of socks in the drawer be?
>b. How small if the number of black socks is even?

抽屉里有红袜子和黑袜子，随机抽出两只，两只全红的概率为 1/2

问:
a. 抽屉里的袜子最少有多少只
b. 如果黑袜子为偶数只，则抽屉里的袜子最少有多少只

# 思路参考

## a 

设抽屉里有 x 只红袜子，y 只黑袜子，总共 N = x + y 只袜子，记随机抽两只均为红色的概率为 P

$$
P = \frac{\binom{x}{2}}{\binom{x+y}{2}} = \frac{x(x-1)}{(x+y)(x+y-1)} = \frac{1}{2} \\
\Rightarrow 2x(x-1) = N(N-1)
$$

问题变成解以上不定方程 N > 2 的最小正整数解

### 解析解

由于对于 y > 0, x > 1，有以下不等式

$$
\frac{x}{x+y} > \frac{x-1}{x+y-1}
$$

再结合

$$
\frac{\binom{x}{2}}{\binom{x+y}{2}} = \frac{x(x-1)}{(x+y)(x+y-1)} = \frac{1}{2}
$$

我们可以得到不等式

$$
(\frac{x}{x + y})^{2} > \frac{1}{2} > (\frac{x-1}{x+y-1})^{2} \\
\Rightarrow  \frac{x}{x + y} > \frac{1}{\sqrt{2}} > \frac{x-1}{x+y-1}
$$

从左半部分不等式可以计算出

$$
(\sqrt{2} + 1)y < x
$$

从右半部分不等式可以计算出

$$
x < (\sqrt{2} + 1)y + 1 
$$

因此对于 y = 1, x 的范围在 $[1 + \sqrt{2}, 3 + \sqrt{2}]$，所以 x = 3 是一个候选答案

### 数值解

暴力解法代码如下, 从 y = 1, x = 2 开始枚举，判断是否满足方程。

```python
y = 1
found = False
while True:
    x = 2
    while True:
        N = x + y
        if 2 * x * (x - 1) == N * (N - 1):
            print("N: {}, x: {}".format(x, N))
            found = True
            break
        elif 2 * x * (x - 1) > N * (N - 1):
            break
        x += 1
    if found:
        break
    y += 1
```

得到 N = 4, x = 3

## b

### 解析解

利用在此前已经推出的以下公式

$$
(\sqrt{2} + 1)y < x < (\sqrt{2} + 1)y + 1 
$$

这里规定了 y 是偶数。依次考虑 y = 2, 4, 6, ...，对每一个 y，我们可以知道 x 的范围，这个范围的长度正好为 1，因此也就是可以知道对应的 x 具体是多少。考察这对 (x, y) 是否满足 P = 1/2 即可。

第一个满足的就是答案。

### 数值解

依然用暴力法解，只需要把 y 的初始值改为 2, 每轮 y 的增加量改为 2 即可

```python
y = 2
found = False
while True:
    x = 2
    while True:
        N = x + y
        if 2 * x * (x - 1) == N * (N - 1):
            print("N: {}, x: {}".format(x, N))
            found = True
            break
        elif 2 * x * (x - 1) > N * (N - 1):
            break
        x += 1
    if found:
        break
    y += 2
```

得到 N = 21, x = 15
