
# 写在前面

本题来自 《Fifty challenging problems in probability with solutions》。

---

# 问题描述

>A 3 man jury has 2 members each of whom independently has probability p of making the correct decision, and a 3rd member who flips a coin for each decision
>A one man jury has probability p of making the correct decision
>Which jury has the better probability of making the correct decision?

有一个3人组成的陪审团，其中两个人独立做决定均有 p 概率做对，另一个人通过抛硬币做决定
还有一个1人的陪审团，那个人做决定也有 p 概率做对
问哪个陪审团更优可能做出正确决定

# 思路参考

第一个陪审团做出正确决定的概率记为 P1, 第二个陪审团做出正确决定的概率记为 P2

$$
P1 = p \\
P2 = p \times p + 2 \times p \times (1 - p) \times \frac{1}{2} = p
$$

因此 P1 = P2，两个陪审团做出正确决定的可能性相等。

## 构造数据验证

```python
T = 10
n_trails = int(1e6)

for t in range(T):
    p = np.random.random()
    # 模拟第一个陪审团 3 个人各自做出的判断，1为正确判断
    # 模拟 n_trails 次
    c1 = np.random.binomial(1, p, size=n_trails)
    c2 = np.random.binomial(1, p, size=n_trails)
    c3 = np.random.binomial(1, 0.5, size=n_trails)
     # c 中记录了 n_trails 次模拟中每次是否做出了正确判断
    c = ((c1 + c2 + c3) >= 2).astype(int)
    print("P2 = {:.5f}, P1 = {:.5f}".format(p, np.mean(c)))
```

实验结果

```plain
P2 = 0.34158, P1 = 0.34095
P2 = 0.55780, P1 = 0.55776
P2 = 0.07460, P1 = 0.07439
P2 = 0.01918, P1 = 0.01919
P2 = 0.39175, P1 = 0.39233
P2 = 0.82699, P1 = 0.82643
P2 = 0.84726, P1 = 0.84769
P2 = 0.00396, P1 = 0.00395
P2 = 0.09100, P1 = 0.09023
P2 = 0.45738, P1 = 0.45741
```
