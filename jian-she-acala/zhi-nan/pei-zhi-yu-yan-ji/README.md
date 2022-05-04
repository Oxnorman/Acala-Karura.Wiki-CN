# 配置预言机

## 服务提供商的设置

一个预言机网络提供商将部署他们自己的预言机Pallet（基于 [默认预言机pallet](https://github.com/open-web3-stack/open-runtime-module-library/tree/master/oracle)) 来实现他们特定的需求，比如验证跨链数据推送。我们可以轻松与现有的签名预言机API进行集成，比如 [Coinbase 价格预言机](https://blog.coinbase.com/introducing-the-coinbase-price-oracle-6d1ee22c7068) 。方法很简单，添加Coinbase提供商的Pallet以及验证他们的签名。

然后添加预言机服务提供商到Runtime中（详见[Acala 预言机](https://github.com/AcalaNetwork/Acala/blob/master/runtime/mandala/src/lib.rs#L447)) ，在runtime升级中会发布此项功能。

### 设置运行人节点

一个服务商可以在其预言机网络中添加多个运行人节点，运行人节点的[例子](https://github.com/laminar-protocol/oracle-server)。

## 加入开放式预言机网关

预言机网关部署和运行于Acala的Mandala测试网上。除了Acala团队和Laminar团队，Band协议团队对网关的开发做出了贡献。我们希望网关能够成为Acala，Polkadot，Kusama以及整个Defi跨链生态的基于公共利益的基础设施。因此我们欢迎预言机服务提供商能够查阅我们的网关代码，与我们讨论集成的可能，贡献一些力量到代码库中并且为持续成长的生态系统提供服务。&#x20;

&#x20;**在Acala/Karura创世之前**

* 请直接与我们联系或者在 [Discord](https://discord.gg/vdbFVCH) 表示你对我们感兴趣
* 提出Pull请求
* 我们将查阅，批准Pull 请求
* 然后将代码融合和部署到测试网上&#x20;

**在Acala/Karura创世之后**

* 请联系Acala/Karura 理事会来表达兴趣和寻求批注
* 批准之后，提出Pull请求
* 代码审阅和添加
* runtime 升级
