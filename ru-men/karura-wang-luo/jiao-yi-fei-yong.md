# 交易费用

**🔔 Karura允许任何支持的token作为支付费用。** 然而转账刚开启时，会有一段时间交易费用只能用原生token KAR来进行支付，直到KSM/KAR, kUSD/KAR 和其他Karura Swap池子开启bootstrap，然后KSM，aUSD以及其他token才能被用作交易费用。

交易费的使用是为了防止一些用户占据过多有限的区块链资源，比如存储和计算资源。Karura使用具有权重的费用，这点与Gas费不同，它是可预见的并且在调度前收取。

### 费用预估

如下是对一个典型交易费用的粗略估计：

* **从Kusama转账到Karura，**这种跨链转账费用分为两部分：
  * Kusama费用, 由Kusama决定
  * Karura费用: 0.3 milliKSM\~
* **从Karura转账到Kusama,** 这种跨链转账费用分为两部分：
  * Karura费用: 4 milliKAR (0.004 KAR)\~
  * Kusama费用, 由Kusama决定
* **Karura**&#x20;
  * **转账:** 4 milliKAR (0.004 KAR)\~
  * **DeX兑换:** 12 milliKAR\~
  * **添加流动性:** 18 milliKAR\~
  * **调整aUSD贷款:** 18 milliKAR\~

请注意：这些都是估计数额，收取的费用会根据真实的转账规模，网络状况以及其他因素进行重新计算。

现在来说，所有的交易费用都收归于Karura国库- 微小的贡献来实现一个可持续的未来。更多信息请点击[这里](jiao-yi-fei-yong.md)

### 费用调整 <a href="#fee-adjustment" id="fee-adjustment"></a>

在Karura上费用的调整是基于实际交易量，同时也是可预见的。Karura有区块填充上限，费用会根据下一个区块的填充度与填充上限之间的差值来调整。

### 带上你自己的Gas费

为什么要要求用户在转账其他token时，必须用网络的原生token来支付交易费用？！在Karura上，你就有你的自由。用户可以用任何网络支持的token来支付费用。用户在用除了KAR以外的其他token支付时，费用本身还是以KAR进行计价的，一个实时兑换操作（用于支付的token和KAR之间）被链自动执行了。该操作原子级别的并且用户可见。
