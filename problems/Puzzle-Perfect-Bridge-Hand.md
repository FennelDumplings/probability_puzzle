---
top: 0
title: 【Puzzle】完美手牌
abbrlink: c5969f62
date: 2021-06-26 10:48:32
tags:
  - 概率
  - Puzzle
categories:
  - 数
  - 概率
thumbnail: https://i.loli.net/2021/05/25/FXob8M72YK1nhLD.jpg
---

这是概率面试题连载第 10 期，我们继续看 《Fifty challenging problems in probability with solutions》 中的一道题。

往期的内容整理在这个 github 仓库里 [probability_puzzle](https://github.com/FennelDumplings/probability_puzzle)。

---

# 问题描述

>Puzzle-Perfect-Bridge-Hand
>-
>We often read of someone who has been dealt 13 spades at bridge
>With a well-shuffled deck of cards, what is the chance that you are dealt a perfect hand (13 of one suit)?

从一副洗好的牌(52张)中抽 13 张，拿到完美手牌(拿到的 13 张是同花色)的概率是多少。

# 思路参考

52 张牌一共有 52! 中排列顺序。

完美手牌需要抽取的 13 张是同一花色，这 13 张同一花色的牌有 13! 种排列顺序，未被抽到的 39 张牌有 39! 中排列顺序。

因此对于指定花色，所有抽到的牌都是这一指定花色的概率为

$$
p = \frac{13! \times (39)!}{52!} 
$$

一共有四种花色，因此拿到完美手牌的概率为

$$
4p = \frac{4 \times 13! \times (39)!}{52!}
$$

编程计算

```python
from math import factorial as fac

p = 4.0 * fac(13) * fac(39) / fac(52)
print("{:.6e}".format(p))
```

计算结果

```plain
6.299078e-12
```

