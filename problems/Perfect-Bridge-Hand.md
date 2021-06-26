# 写在前面

本题来自 《Fifty challenging problems in probability with solutions》。

---

# 问题描述

>Puzzle-Perfect-Bridge-Hand
>--
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

