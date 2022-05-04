# 工具

## 区块浏览器

* [Polkadot 浏览器 ](https://polkadot.js.org/apps/#/explorer) - Acala控制面板的浏览器。目前默认连接到Acala，但可以配置为连接到其他远程或本地端点。
* [Polkascan](https://polkascan.io) - Polkadot, Kusama, 其他相关链的区块链浏览器
* [Subscan](https://subscan.io) - 为Substrate链的区块链浏览器，包括Acala。

## Wallets

> 集成Acala‘的钱包可以非常简单便捷的使用私钥和签署交易。下面是一些支持Acala的钱包以及他们的一些发展状况。请注意，列入的钱包并不代表对他们的认可。

### 支持的钱包

| 钱包名称                                                           | 开发状态     | 团队名称        | Description       |
| -------------------------------------------------------------- | -------- | ----------- | ----------------- |
| [Acala DApp](https://apps.acala.network)                       | Live     | Acala       | Browser           |
| [Polkadot Explorer](https://polkadot.js.org/apps/)             | Live     | Acala       | Browser           |
| [Polkawallet](https://polkawallet.io)                          | Live     | Polkawallet | IOS and Android   |
| [Signer](https://www.parity.io/signer/)                        | Building | Parity      | IOS and Android   |
| [Polkadot-JS](https://polkadot.js.org/apps/#/accounts)         | Building | Parity      | Browser           |
| [Polkadot.JS Plugin](https://github.com/polkadot-js/extension) | Building | Parity      | Browser extension |

## Network Monitoring & Reporting

* [Polkadot Telemetry服务 ](https://telemetry.polkadot.io) - 网络信息包括哪些节点正在运行链、这些节点正在运行软件的什么版本、同步状况以及位置。

## 库

* [acala.js](https://github.com/AcalaNetwork/acala.js) - 该SDK是 [polkadot.js](https://github.com/polkadot-js/api)的扩展，具有额外的类型和元数据信息，使用户可以轻松与Acala网络互动。

## 数据分析

* [@acala-weaver/graphql-server ](https://github.com/AcalaNetwork/chain-sync-server/tree/master/packages/graphql-server)- 支持一个基于graphQL的查询服务器
* [@acala-weaver/chain-recoder](https://github.com/AcalaNetwork/chain-sync-server/tree/master/packages/chain-recoder) - 同步链和维护账户，DCP等等。
* [@acala-weaver/storage-recoder](https://github.com/AcalaNetwork/chain-sync-server/tree/master/packages/storage-recoder) - 将链上存储的数据同步到时间序列的数据库中，用于监测和报警。

## Faucet

* [Faucet-bot](https://github.com/AcalaNetwork/faucet-bot) -  Riot的代码和 Discord faucet bot.
* [Discord Faucet Channel ](https://discord.gg/V8XgJ5)- Discord faucet channel.
* [Riot Faucet Channel](https://riot.im/app/#/room/#acala-faucet:matrix.org) - Riot faucet channel.

## 抵押品拍卖&清算机器人

当前接我们有两个机器人来监控流动性拍卖。

* [为](https://github.com/open-web3-stack/guardian/tree/master/packages/example-guardian#collateral-auction-bot-for-acalakarura)[Acala/Karura的抵押品拍卖机器人](https://github.com/open-web3-stack/guardian/tree/master/packages/example-guardian#collateral-auction-bot-for-acalakarura) -这个例子使用抵押品拍卖。如果抵押品的价格低于来自基于MARGIN相关系数的预言机价格，它将开始监控抵押品拍卖和DEX池子以及指定的账户竞价。
* [抵押拍卖机器人案例](https://github.com/AcalaNetwork/collateral-auction-bot-example)- 这是拍卖机器人的例子，以LKSM为抵押品的铸币池变为非安全铸币池，开启清算，拍卖机器人对向清算过程出价。

## EVM 工具

* [EVM 游乐场](https://evm.acala.network) - 一个网页应用来测试，部署以及执行在Acala EVM上的智能合约
