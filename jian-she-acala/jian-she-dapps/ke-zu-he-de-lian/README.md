# 可组合的链

当前，跨链消息传递以及平行链在Polkadot/Kusama上已经得到实现。

Acala/Karura已经在Polkadot/Kusama上面启动，并且正在测试跨链的同质化Token的转账以及其他功能。

如果你需要帮助，请通过[Discord 技术聊天室](https://discord.com/invite/Xb3CxcjCVc)来与我们沟通

## 与Acala融合

* 在Kusama上的[Karura](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkusama-rpc.polkadot.io#/parachains)已经上线
* 在Polkadot上的[Acala](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.polkadot.io#/parachains)已经上线

### 背景

Polkadot[跨共识信息格式（XCM)](https://github.com/paritytech/xcm-format)是一种通用的消息格式，他并不需要想同质化Token那样有确定的用例。因此，我们需要提供一个所需用例的实现（比如跨链转账），让平行链在相同环境下实现互操作，比如说，在平行链之间和平行链与中继链之间，发送或接受同质化资产。我们希望对于中继链的资产（比如DOT或者KSM）和对原生平行链资产（比如Acala的ACA和Karura的KAR）保持相同的接口，然后将实现的细节进行抽象，来让开放人员更容易的集成。

[XCM同质化资产实施指南](https://github.com/open-web3-stack/open-runtime-module-library/discussions/385)阐述了跨链同质化资产的设计考虑和讨论，以及Acala和其他许多开发团队目前正在采用和测试的orml-xtokens。&#x20;

每个平行链都有自己的同质化token，对于想要对其资产和其他平行链token进行跨链转移的平行链来说，[`orml-xtokens`](https://github.com/open-web3-stack/open-runtime-module-library/discussions/385)是XCM对同质化token的实施参考，可以帮助轻松完成跨链token转移工作。

> 请注意: 这个实施参考不是绝对的，而是平行链社区进行试验和迭代的起点。请提供关于 [`xtokens`](https://github.com/open-web3-stack/open-runtime-module-library/tree/master/xtokens) 或者 [implementation guide](https://github.com/open-web3-stack/open-runtime-module-library/discussions/385) 的反馈。

平行链有自己的实施方案，不仅管理本身的资产，也管理外部资产。目前，Acala使用[资产注册表](https://github.com/AcalaNetwork/Acala/tree/master/modules/asset-registry)。因此，对于想加入Acala或Karura的平行链，请参考[这里](https://app.gitbook.com/s/I60OMjSmrBgy1AoE1I84/kai-fa-zhe-zhi-nan/chuang-jian-yi-ge-xin-token)的用户指南。其他的parachain可能有不同的资产管理（例如，基于Substrate的Pallet资产）或只是手动维护资产，但他们都使用`orml-xtokens`进行跨链Token转账。

## 集成指南

### 步骤 0 本地平行链测试

请阅读[Acala主repo](https://github.com/AcalaNetwork/Acala)的Readme文件，设置一个本地平行链测试环境有两种方式：

* 使用平行链启动，与Docker一同运行，请按照[指南](https://hackmd.io/dhmCATb\_QqygCPxkxaDcmA)操作（指南由@bertstachios提供）
* 使用Polkadot启动，与二进制建设发布文档一同运行

### 步骤 1 集成`xtokens`模块支持Acala/Karura Tokens

要接收Acala链（aUSD, ACA, renBTC, LDOT等）或Karura链（aUSD, KAR, LKSM等）上发行的token，你需要在你的货币类型中包含它们；同时，需要实现货币ID转换。查看Acala运行时的货币ID转换的[例子](https://github.com/AcalaNetwork/Acala/blob/2.3.1/runtime/acala/src/lib.rs#L1700-L1814)。

> `CurrencyIdConvert` 可以将`CurrencyId` 转换成`MultiLocation`并且可以实现`MultiLocation`转成`CurrencyId`。前者的转换使用orml-xtoken来发送xcm到接收链，但后者是当你接收到需要转到正确token的xcm指令时使用

### 步骤 2 将你的token上到Acala/Karura

有一个启动程序来在Acala/Karura上引进新token同时避免垃圾token的进入。Acala采用[资产注册](https://github.com/AcalaNetwork/Acala/tree/master/modules/asset-registry)的方式来管理资产，更多详细信息请参考[使用指南](https://app.gitbook.com/s/I60OMjSmrBgy1AoE1I84/kai-fa-zhe-zhi-nan/chuang-jian-yi-ge-xin-token)，这里有关于添加新token到Acala/Karura上的指导。

### 步骤 3 开启HRMP信道

> 如果你使用parachain-launch或者Polkadot-launch，两种工具都支持在启动本地测试网时，初始化HRMP信道，所以跨链token的转账已准备就绪。当然你也可以通过如下指示，手动初始化HRMP信道。

当前你的链应该已经作为平行链连接到Polkadot/Kusama上了。当XCM（跨链消息传递）仍在实施中-即不能通过中继链直接发送跨链消息，一个权宜之计的协议-HRMP（水平中继路由消息传递）-作为暂时替代方案已经就位。

> HRMP具有与XCMP相同的接口和功能，但对资源的要求要高得多，因为它把所有的消息都存储在中继链的存储器中。当XCMP实现后，HRMP计划被废弃并逐步淘汰，以支持XCMP。

两个平行链都需要开启HRMP通道来发送和接收跨链信息。[这里有打开HRMP通道的说明。](kai-qi-hrmp-xin-dao.md)

Polkadot/Kusama上的所有链应可相互组合，从交换价值到交换和改变状态。例如，链不仅可以无信任地转移价值，还可以相互调用 Pallet/智能合约功能，例如在Interlay链上铸造Polkabtc，将Polkabtc转移到Acala，并将其抵押给aUSD，所有这些都在一次交易中实现。&#x20;

Acala将与以下（潜在的）平行链进行组合。如果你有或正在实施xtokens，请PR（拉取请求）到这个Repo，然后添加自己项目。

* Bifrost
* Astar
* Interlay
* Phala
* Moonbeam
* Centrifuge
* HydraDX
* Darwinia
* Kilt
* Crust
* Snowfork
* Bit.Country
* ...

如果你想尝试一下，需要支持，和/或想和我们一起进行一些跨链测试，请不要犹豫，与我们联系!
