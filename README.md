# 写在前面

现在的技术岗位面试中，大部分公司都会问道概率相关的问题。比如互联网公司的研发工程师，算法工程师，算法研究员，数据分析师，以数据驱动为核心的公司的风控/营销相关的岗位等等。特别是算法工程师和数据分析师，如果工龄较短或者是校招，几乎是必考。

本仓库持续更新【概率计算】问题及解答。主要来源是一些书、我和周围朋友面试遇到的题以及网上的零散面经中觉得还不错的题。

对于每道题，首先给出思路参考，从概率论的角度推公式求解。然后用蒙特卡洛模拟的方式验证结果，编程语言用的是 Python。

如果有问题可以 [联系我](https://chengzhaoxi.xyz/algorithm_tss/index.html) 进行沟通交流。

# 参考书

- [《Fifty challenging problems in probability with solutions》](https://book.douban.com/subject/2193302/)
- [《40 Puzzles and Problems in Probability and Mathematical Statistics》](https://book.douban.com/subject/10124106/)

---

# 已更新题目汇总

由于 github 的 markdown 不支持 LaTeX 公式，因此链接给的是我的网站的链接，阅读效果更好。

| 编号 | 题目                                                                     | 备注                     |
| --   | --                                                                       | -                        |
| 1    | [抽屉中的袜子](https://chengzhaoxi.xyz/5b96d3b7.html)                    | -                        |
| 2    | [系列赛中连续获胜](https://chengzhaoxi.xyz/7baa7d02.html)                | -                        |
| 3    | [轻率的陪审团](https://chengzhaoxi.xyz/562429f2.html)                    | -                        |
| 4    | [三人循环赛](https://chengzhaoxi.xyz/5ddc2958.html)                      | -                        |
| 5    | [试验直到第一次成功](https://chengzhaoxi.xyz/a8fe89ba.html)              | -                        |
| 6    | [公司从用户一次游戏取得的收入](https://chengzhaoxi.xyz/cbac9217.html)    | 全期望公式、期望DP       |
| 7    | [向正方形区域扔硬币](https://chengzhaoxi.xyz/ecb676f8.html)              | -                        |
| 8    | [祝你好运](https://chengzhaoxi.xyz/997685ba.html)                        | -                        |
| 9    | [资助赌徒](https://chengzhaoxi.xyz/b39ddb37.html)                        | -                        |
| 10   | [完美手牌](https://chengzhaoxi.xyz/c5969f62.html)                        | -                        |
| 11   | [双骰子赌博](https://chengzhaoxi.xyz/d8864c7f.html)                      | -                        |
| 12   | [收集优惠券](https://chengzhaoxi.xyz/3b094aed.html)                      | 设计随机变量、全期望公式 |
| 13   | [一排座位](https://chengzhaoxi.xyz/45af2f3.html)                         | 全期望公式、期望DP       |
| 14   | [第二强的选手是否拿亚军](https://chengzhaoxi.xyz/26b83c46.html)          | -                        |
| 15   | [孪生骑士](https://chengzhaoxi.xyz/9e8462fe.html)                        | 条件概率                 |
| 16   | [塞缪尔·佩皮斯的问题](https://chengzhaoxi.xyz/f7d03b7c.html)             | 全概率公式、概率DP       |
| 17   | [三人枪战](https://chengzhaoxi.xyz/6e9feb0d.html)                        | -                        |
| 18   | [不公平的硬币](https://chengzhaoxi.xyz/52c92ad.html)                     | 贝叶斯公式               |
| 19   | [不公平的硬币2](https://chengzhaoxi.xyz/b2b74dca.html)                   | 贝叶斯公式               |
| 20   | [不公平的硬币3](https://chengzhaoxi.xyz/c5b07d5c.html)                   | 贝叶斯公式               |
| 21   | [不公平的硬币4](https://chengzhaoxi.xyz/5bd4e8ff.html)                   | 贝叶斯公式               |
| 22   | [有放回抽样还是无放回抽样](https://chengzhaoxi.xyz/f905bb10.html)        | 贝叶斯公式               |
| 23   | [圆周上随机取3个点形成锐角三角形](https://chengzhaoxi.xyz/19bd5f5f.html) | 几何概型                 |
| 24   | [选票盒](https://chengzhaoxi.xyz/f0f7c7a1.html)                          | 概率DP                   |
| 25   | [系列赛中不出现平局](https://chengzhaoxi.xyz/8d5da794.html)              | 概率DP                   |
| 26   | [仓促的决斗](https://chengzhaoxi.xyz/e72d925c.html)                      | 几何概型                 |
| 27   | [较短的一节木棍](https://chengzhaoxi.xyz/ca9456d5.html)                  | 连续型随机变量           |

