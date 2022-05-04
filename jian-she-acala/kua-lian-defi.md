# 跨链Defi

## Acala的跨链Defi

Acala是一个DeFi分片 ，也就是Polkadot的多链世界的金融中心。Acala提供了一整套金融产品基础组件，包括多抵押品的稳定币，无需信任抵押衍生品和一个去中心化交易所。这些产品基础组件通过Acala的DApp直接提供给终端用户，同时也作为SDK提供给更多的DApp使用。我们可以预见到一个更加互联的、自主的、更复杂的、跨区块链的金融生态系统正在孕育之中。&#x20;

这里我们将介绍与Acala合作和实验的项目。

### Laminar

Laminar链是一个基于Substrate的专业、高性能的合成资产和基于保证金的交易链。它将使用Acala Dollar（代码：aUSD）作为其基础交易货币，以铸造欧元和日元等合成稳定币。它还引入了各种交易工具，包括各种资产的杠杆交易，比如外汇对、黄金、股票以及合成加密货币对，例如BTC/USD和ETH/USD。价值转移（现阶段为aUSD）将实施一个社区接受的[代币标准](https://github.com/w3f/PSPs/pull/3)。

### Ren

Ren是一个有信誉的、区块链间的资产桥，目前资产类型有BTC、BCH和ZEC，丰富了以太坊的DeFi应用场景。Ren[通过在Acala网络](https://github.com/AcalaNetwork/Acala/wiki/U.-Build-with-Acala)上部署其[RenVM桥接模块](https://github.com/AcalaNetwork/Acala/tree/master/ecosystem-modules/ren/renvm-bridge)，与Acala建立了联系。BTC网关由RenVM提供，在Acala上铸造和燃烧renBTC由该网关模块提供。Ren用户在前期将享受一些如下好处：

1. 一个全新的账户，只有新铸造的renBTC，可以在Acala上进行任何交易，而不需要手续费。由于Acala的灵活收费功能，像renBTC这样的token被原生地整合为默认收费token之一，与ACA、aUSD和DOT并列。&#x20;
2. 为了促进renBTC在Acala和更广泛的Polkadot生态系统中的使用，可以在不影响安全性的情况下免除铸造renBTC的费用。&#x20;

对于考虑进入Polkadot的多链生态系统的DeFi项目来说，Ren是一个很好的例子，利用Acala的定制/优化的金融平台，无需为建立一个单独的区块链（或所谓的平行链）承担前期经济和技术负担。&#x20;

## Mandala测试网络&#x20;

在Mandala测试网络上，跨链功能由一个可信的服务商提供，并将在Polkadot的XCMP（跨链消息传递）机制可用时，使用XCMP。

### Laminar链

![lamianr](https://github.com/AcalaNetwork/Acala/wiki/image/cross-laminar.png)

* [Laminar Flow Exchange](https://flow.laminar.one)
* [入门](https://github.com/laminar-protocol/laminar-chain/wiki/1.-Get-Started)
* [视频:保证金交易](https://youtu.be/s4pl6glM5kA)

#### 转账aUSD到Laminar链上

前往 `Wallet` --> 页面 `Cross-chain` --> 选择 `Inter Polkadot Transfer`. 然后选择 `To Chain` "Laminar", 设置货币单位为 "aUSD" 然后填入转账接收账户然后输入你想发送的aUSD数量，点击 `Transfer`. aUSD将会按照要求的数量转账到  Laminar链上.

![transfer](https://i.imgur.com/0hcakPv.png)

#### 将 aUSD 从 Laminar 链上转账回来

![transferback](https://github.com/AcalaNetwork/Acala/wiki/image/cross-laminartoacala.png)

在 [Laminar Flow Exchange](https://flow.laminar.one), 前往 `Dashboard` --> 点击aUSD旁的 `transfer` , 填入你希望发送到Acala的aUSD数量，然后点击 `Confirm`.  aUSD 会发送到 Laminar 链上相同的账户.

### Ren

![lamianr](https://github.com/AcalaNetwork/Acala/wiki/image/cross-renbtc.png)

#### Minting renBTC

在Mandala测试网上, 池口每次流入0.2个renBTC, 上限为 1 renBTC/月/用户. 在金丝雀网络和测试网上，RenVM 将被用于铸造和燃烧renBTC.

![laminar](https://i.imgur.com/mCAKXyF.png)

#### 使用renBTC

与Ren的合作将促进Acala上的可用资产类别，并为比特币带来全新的使用案例：

* renBTC可以作为aUSD信用贷款的抵押品&#x20;
* renBTC可以在Acala DeX上交易其他资产，如DOT、LDOT、ACA、aUSD、XBTC。&#x20;
* 用户现在可以通过交易DOT和使质押衍生品协议，来参与Polkadot PoS验证并获得质押奖励
* 为DeX提供流动性并赚取额外的收益已经是成熟的流程
* aUSD可以转移到Laminar Chain，用于保证金交易合成外汇对，如EURUSD，黄金和股票，以及合成BTC和ETH。

