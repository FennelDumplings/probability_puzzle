# 写在前面

本题来自 《Fifty challenging problems in probability with solutions》。

---

# 问题描述

>Curing-the-Compulsive-Gambler
>--
>Mr. Brown always bets a dollar on the number 13 at roulette against the advice of Kind Friend
>To help cure Mr. Brown of playing roulette, Kind Friend always bets Brown $20 at even money that Brown will be behind at the end of 36 plays
>How is the cure working?
>(Note: Most American roulette wheels have 38 equally likely numbers. If the player's number comes up, he is paid 35 times his stake, plus he gets his original stake back. Otherwise, he loses his stake)

布朗沉迷于轮盘赌，并且强迫症地总是在13这个数字上押注1美元。

好朋友为了资助布朗，与布朗等额投注 20 美元(好朋友和布朗均需要出 20 美元)，赌以下事情: 布朗在第 36 次游戏完成之后会亏钱(如果果真亏钱了，则朋友得到双方的筹码共 40 美元，否则布朗得到这 40 美元)。

轮盘赌有 38 个等概率的数字，如果玩家押注的数字出现，则拿到 35 倍投注金额，加上原始投注金额，共 36 倍，如果押注的数字没出现，则损失原始投注金额。

问：这个帮助措施是否有效，即好朋友和布朗期望会挣钱。

# 思路参考

布朗每次游戏的获胜概率为 p = 1/38，期望从赌场拿回的钱为 `36 * p`。

考虑 36 次游戏。布朗需要付出 36 美元与赌场的押注金额，以及 20 美元与朋友的押注金额。下面我们看布朗期望能够拿回多少钱。

布朗拿回的钱中，一部分来自赌场，另一部分来自朋友。

来自赌场的部分，布朗每次期望拿回 `36 * p`，36 次期望拿回 `36 * 36 * p`。

下面考虑来自朋友的部分:

每一次获胜，布朗会获得 36 美元。也就是说布朗只要赢一次就已经不亏了，也就意味着朋友只要不是 36 场全输了，就可以从朋友那里拿回 40 美元。

布朗在 36 次游戏中至少赢一次的概率为:
$$
1 - (1 - p)^{36}
$$

因此布朗期望从好朋友那里拿回的金额为 `40 * (1 - (1 - p) ^ 36)`

把两部分加在一起，布朗在 36 次游戏中期望拿回的金额为

$$
E = 40(1 - (1 - p)^{36}) + 36 \times 36 \times p
$$

这个数只要大于 36 + 20 = 56 美元，那么朋友的这个帮助措施就有效。下面我们编程计算这个数

```python
def E(p):
    q = (1 - p) ** 36
    return 40 * (1 - q) + 36 * 36 * p

income = E(1 / 38)
print("Except Income: {:.6f}".format(income))
```

计算结果

```plain
Except Income: 58.790419
```

由于期望能拿回 58.790419 美元，比 56 美元多，朋友的资助有效。

# 蒙特卡洛模拟

```python
from multiprocessing import Pool
import numpy as np

p = 1/38

def game1():
    # 1 次游戏，返回游戏结束拿回的钱
    if np.random.rand() < p:
        return 36
    return 0

def game36():
    # 36 次游戏，返回36次游戏结束拿回的钱
    w = 0
    for _ in range(36):
        w += game1()
    if w >= 36:
        return w + 40
    return w

def test(T):
    np.random.seed()
    total = 0
    for _ in range(T):
        total += game36()
    return total / T

T = int(1e6)
args = [T] * 8
pool = Pool(8)
incomes = pool.map(test, args)
for x in incomes:
    print("Average Income: {:.6f}".format(x))
```

模拟结果

```plain
Average Income: 58.894648
Average Income: 58.697580
Average Income: 58.741948
Average Income: 58.745660
Average Income: 58.757380
Average Income: 58.819856
Average Income: 58.800196
Average Income: 58.767288
```

