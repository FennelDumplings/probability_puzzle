
# 写在前面

本题来自 《Fifty challenging problems in probability with solutions》。

---

# 问题描述

>Chuck-a-luck is a gambling game often played at carnivals and gambling houses
>A player may bet on any one of the numbers 1, 2, 3, 4, 5, 6
>
>Three dice are rolled
>
>If the player's number appears on one, two, or three of the dice, he receives respectively one, two, or three times his original stake plus his own money back
>Otherwise, he loses his stake
>
>What is the player's expected loss per unit stake?

"祝你好运"一种赌博游戏，经常在嘉年华和赌场玩。

玩家可以在 1, 2, 3, 4, 5, 6 中的某个数上下注。然后投掷 3 个骰子。

如果玩家下注的数字在这三次投掷中出现了 x 次，则玩家获得 x 倍原始投注资金，并且原始投注资金也会返还，也就是总共拿回 (x + 1) 倍原始投注资金。如果下注的数字没有出现，则原始投注资金不会返还。

问：每单位原始投注资金，玩家期望会输多少。

# 思路参考

设原始投注资金为 s，下注的数字在三次投掷中出现了 x 次，x 的取值为 0, 1, 2, 3，下面我们分别考虑这四种情况。

$$
P(x = 3) = (\frac{1}{6})^{3} = \frac{1}{216}\\
P(x = 2) = \binom{3}{1} \times \frac{5}{6} \times (\frac{1}{6})^{2} = \frac{15}{216} \\
P(x = 1) = \binom{3}{2} \times (\frac{5}{6})^{2} \times \frac{1}{6} = \frac{75}{216} \\
p(x = 0) = (\frac{5}{6})^{3} = \frac{125}{216} \\
$$

按照期望的定义

$$
E(X) = \sum\limits_{i} i \times p(i)
$$

拿回的钱的期望为 

$$
\begin{align}
E &= 4s \times P(x = 3) + 3s \times P(x = 2) + 2s \times P(x = 1) \\
&= 4s \times \frac{1}{216} + 3s \times \frac{15}{216} + 2s \times \frac{75}{216} \\
&= \frac{4 + 45 + 150}{216}s = \frac{199}{216}s
\end{align}
$$

每单位投注资金的损失为 `17/216 = 0.0787`

# 蒙特卡洛模拟

```python
import numpy as np

def game():
    x = 0
    for _ in range(3):
        if np.random.randint(1, 7) == 1:
            x += 1
    if x == 0:
        return 0
    return x + 1

def test():
    T = int(1e6)
    total_income = 0
    for t in range(T):
        total_income += game()
    print("expected loss: {:.6f}".format((T - total_income) / T))

for i in range(10):
    test()
```

模拟结果

```plain
expected loss: 0.078817
expected loss: 0.078182
expected loss: 0.078731
expected loss: 0.078875
expected loss: 0.078526
expected loss: 0.078657
expected loss: 0.078634
expected loss: 0.079033
expected loss: 0.079353
expected loss: 0.079307
```

