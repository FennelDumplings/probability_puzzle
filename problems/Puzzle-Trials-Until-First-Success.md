---
top: 0
title: 【Puzzle】Trials-Until-First-Success
abbrlink: a8fe89ba
date: 2021-05-27 16:51:31
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

>On average, how many times must a die be thrown until one gets a 6?

一枚骰子掷出第一个 6 平均需要掷多少次。

# 思路参考1

记 p(k) := 第一个 6 需要掷 k 次的概率。p := 在一次投掷中得到 6 的概率, q = 1 - p

```plain
k = 1: p(1) = p
k = 2: p(2) = pq
k = 3: p(3) = pq^2
...
```

总结规律后可以得到

$$
p(k) = pq^{k-1}
$$

数学期望为

$$
\begin{align}
E(X) &= \sum\limits_{k=1}\limits^{\infty} k \times p(k) \\
&= \sum\limits_{k=1}\limits^{\infty} kpq^{k-1} \\
\end{align} 
$$

处理上面的级数的技巧如下，首先两边都乘以 5/6

$$
\begin{align}
qE(X) &= q\sum\limits_{k=1}\limits^{\infty} kpq^{k-1} \\
&= \sum\limits_{k=1}\limits^{\infty} kpq^{k} \\
\end{align} 
$$

让两式相减

$$
\begin{align}
(1-q)E(X) &= \sum\limits_{k=1}\limits^{\infty} kpq^{k-1} - \sum\limits_{k=1}\limits^{\infty} kpq^{k} \\
&= p + \sum\limits_{k=2}\limits^{\infty} kpq^{k-1} - \sum\limits_{k=1}\limits^{\infty} kpq^{k} \\
&= p + \sum\limits_{k=1}\limits^{\infty} (k+1)pq^{k} - \sum\limits_{k=1}\limits^{\infty} kpq^{k} \\
&= p + \sum\limits_{k=1}\limits^{\infty}pq^{k} \\
&= p\sum\limits_{k=0}\limits^{\infty}q^{k} \\
\end{align} 
$$

其中几何级数那部分的公式如下

$$
\sum\limits_{k=0}\limits^{\infty}q^{k} = 1 + q + q^{2} + ... = \frac{1}{1-q}
$$

将上面的公式代入到两式相减的公式中

$$
pE(X) = p\frac{1}{1-q} = 1 \\
\Rightarrow E(X) = \frac{1}{p}
$$

将 p = 1/6 代入，E(X) = 6

---

# 思路参考2

记 m 为第一个 6 需要的次数

当第一次投掷成功时，则需要的平均次数是 1
当第一次投掷失败时，则需要的平均次数是 1 + m

$$
m = p \times 1 + q \times (1 + m) \\
\Rightarrow m = \frac{1}{p} \\
$$

---

# 蒙特卡洛模拟验证结果

```python
import numpy as np

p = 1/6

def test():
    T = int(1e6)
    mapping = {}
    for t in range(T):
        i = 1
        while True:
            if np.random.rand() < p:
                break
            i += 1
        if i not in mapping:
            mapping[i] = 0
        mapping[i] += 1

    E = 0
    for k in mapping:
        E += k * (mapping[k] / T)
    print("Average times is {:.4f}".format(E))

for i in range(5):
    test()
```

实验结果

```plain
Average times is 6.0025
Average times is 5.9918
Average times is 6.0018
Average times is 6.0038
Average times is 6.0059
```
