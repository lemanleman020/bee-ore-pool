# ore-mine-pool


Ore-Mine-Pool是为OREV2实现的矿池，使矿工更容易挖矿。与 ore-cli 相比，它更易于使用且效率更高。


* ## 使用方法

```c
1. git clone https://github.com/orepool/ore-mine-pool.git
2. cd ore-mine-pool
3. chmod +x start.sh
4. 修改脚本中的solana钱包地址，用于接受ore，需要用户开启ore帐户（考虑私钥安全，所以用户自己创建）。
5  screen -S ore-miner
6. ./start.sh
```


* ## 工作原理


我们运行矿池服务器并使用多个钱包来获取挖矿任务。Miner 每 20 秒从服务器获取难度最低的当前任务，进行 20 秒的计算，并提交获得的最高难度答案。服务器记录难度最高的提交者的钱包。当任务需要在55秒内提交时，最高难度的答案将提交到区块链，并收取矿工费。


* ## 更高的计算效率


使用 ore-cli 进行计算时，挖矿大约需要 55 秒，然后提交需要 1 秒到几分钟，提交后才能继续挖矿。如果每次提交需要 30 秒（这在普通优先权费用下是正常的），效率仅为 55/55+30=64%。使用 ore-miner，我们获取所有的sols，所以再原基础的的情况下我们效率翻倍的增长。


* ## 更好的公交选择


在矿石中，有 8 辆公共汽车（每辆都有 1/8 的奖励容量）。ore-cli 向随机选择的总线提交奖励，但总线之间存在不平衡。如果随机选择的公交车的奖励为零，则提交的奖励将为零。ore-miner选择最佳公交车进行提交（在链上查看最优公交车），确保全额奖励。效率的提高在这里没有量化。


* ## No gas fees


使用 ore-cli 提交奖励会产生 gas 费用，在许多情况下可能会消耗超过 50% 的奖励。使用矿石-矿山-池-工人，天然气费用由我们承担，从而带来 2 倍的收入提高。



* ## 更易于维护


我们处理区块链交互，工作者只需要获取任务、计算和提交答案，无需处理复杂的区块链交互，使其更易于维护。



* ## 安全


只需要钱包公钥，没有私钥泄露的风险。



* ## 费用


矿池费：15%（我们支付汽油费和服务器维护费）
