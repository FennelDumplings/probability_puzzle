
# 写在前面

本题来自 《Fifty challenging problems in probability with solutions》。

---

# 问题描述

>To encourage Elmer's promising tennis career, his father offers him a prize if he wins (at least) two tennis sets in a row in a three set series to be played with his father and the club champion alternately
>
>father-champion-father
>champion-father-champion
>The champion is a better player than Elmer's father
>
>Which series should Elmer choose?

Elmer 如果在三场的系列赛中赢下连续的两场或三场，则可以得到奖励，系列赛的对手安排有两种

1. 爸爸-冠军-爸爸
2. 冠军-爸爸-冠军

这里冠军的水平高于爸爸

问 Elmer 应该选择哪一组，得到奖励的概率更大

---

# 思路参考

一方面，由于冠军水平比爸爸高，应该尽可能少与冠军比赛，另一方面，中间的那一场是更重要的一场，因为如果中间那场输了就不可能连赢两场。

Elmer 与爸爸比赛获胜概率为 P1, 与冠军比赛获胜概率为 P2，由于冠军水平高于爸爸，所以 P1 > P2。

对于一组系列赛，Elmer 要得到奖励有两种可能性，一种是前两场都赢了，此时不用看第三场，另一种是第一场输了，但第二第三场都赢了。

下面分别考虑两组系列赛，计算得到奖励的概率

第一组系列赛，前两场都赢的概率为 `P1 * P2`，第一场输但是第二弹三场都赢的概率为 `(1 - P1) * P2 * P1`，得到奖励概率记为 Pa

$$
Pa = P1 \times P2 + (1 - P1) \times P2 \times P1
$$

第一组系列赛，前两场都赢的概率为 `P2 * P1`，第一场输但是第二弹三场都赢的概率为 `(1 - P2) * P1 * P2`，得到奖励概率记为 Pb

$$
Pb = P2 \times P1 + (1 - P2) \times P1 \times P2
$$

做差比零

$$
\begin{align}
Pa - Pb &= (P1 \times P2 + (1 - P1) \times P2 \times P1) - (P2 \times P1 + (1 - P2) \times P1 \times P2) \\
&= ((1 - P1) - (1 - P2)) \times P1 \times P2 \\
&= (P2 - P1) \times P1 \times P2 \\
&< 0 \\
\end{align}
$$

所以 Pa < Pb，Elmer 应该选择第二组系列赛。

## 构造数据验证

```python
import numpy as np

step = 0.2

for P1 in np.arange(step, 1 + step, step):
    for P2 in np.arange(step, P1 - step, step):
        print("P1: {:.2f}, P2: {:.2f}".format(P1, P2))
        Pa = P1 * P2 + (1 - P1) * P2 * P1
        Pb = P2 * P1 + (1 - P2) * P1 * P2
        print("Pa: {:.2f}, Pb: {:.2f}".format(Pa, Pb))
        print("----")
```

结果如下：可看到 Pb 的值始终比 Pa 大

```plain
P1: 0.60, P2: 0.20
Pa: 0.17, Pb: 0.22
----
P1: 0.60, P2: 0.40
Pa: 0.34, Pb: 0.38
----
P1: 0.80, P2: 0.20
Pa: 0.19, Pb: 0.29
----
P1: 0.80, P2: 0.40
Pa: 0.38, Pb: 0.51
----
P1: 0.80, P2: 0.60
Pa: 0.58, Pb: 0.67
----
P1: 1.00, P2: 0.20
Pa: 0.20, Pb: 0.36
----
P1: 1.00, P2: 0.40
Pa: 0.40, Pb: 0.64
----
P1: 1.00, P2: 0.60
Pa: 0.60, Pb: 0.84
----
P1: 1.00, P2: 0.80
Pa: 0.80, Pb: 0.96
----
```
