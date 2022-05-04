# Token 转账

Acala支持与Polkadot类型不同的Token，并允许以各种方式转移它们。本指南将介绍Acala上可用的Token、可用于转账的工具、如何发送转账交易、监控和跟踪这些交易。

## Token类型

* **原生网络Token**
  * ACA
* **原生协议Tokens**
  * LDOT: 将流动性质押池子里已质押DOT的代币化&#x20;
  * LCDOT: 众贷DOT提取流动性并代币化
  * aUSD: 超额抵押的稳定币
* **外部Tokens**
  * DOT: 从Polkadot中继链跨到Acala
  * 来自其他平行链的Token
  * 来自其他区块链的token，比如ETH, renBTC或 Compound CASH
* **ERC20 Tokens**
  * 通过ERC20合约发行的Token，并部署于Acala EVM

## 工具

* JS/TS SDK: [https://github.com/AcalaNetwork/acala.js](https://github.com/AcalaNetwork/acala.js)
* 区块链浏览器: [http://acala.subscan.io](http://acala.subscan.io)
* api-sidecar: [https://github.com/paritytech/substrate-api-sidecar](https://github.com/paritytech/substrate-api-sidecar)
* txwrapper: [https://github.com/AcalaNetwork/txwrapper](https://github.com/AcalaNetwork/txwrapper)
* SubQuery: [https://github.com/AcalaNetwork/acala-subql](https://github.com/AcalaNetwork/acala-subql)

## Token余额

查询链状态，得到账户余额

### 原生token (ACA) 余额

查询`system` 模块获得原生Token（ACA)的余额数据

#### system.account

* 返回给定账户的 `AccountInfo` 。 对于不同类型的余额，请查询 `AccountInfo.data` 内信息
  * `free`: 不受限的余额.
  * `reserve`: 储备余额.

### 其他tokens

对于非原生token，比如DOT, LDOT, aUSD, 查询 `tokens` 模块，获取余额信息。

#### tokens.accounts

* 返回给定账户的 `OrmlAccountData` 和货币ID. 对于不同类型的余额，对于不同类型的余额，请查询如下数据域
  * `free`: 不受限的余额.
  * `reserve`: 储备余额.

#### tokens.lock

* 返回给定账户的 `BalanceLock` 以及货币ID. `BalanceLock` 有两个数据域:
  * `id`: 锁定标识
  * `amount.` 锁定的数量.
* 请注意可能存在多重锁定，相同数量的token可能被多个锁进行锁定。

## 发送Tokens

### 交易

#### currencies.transfer

* [https://acala.subscan.io/extrinsic?module=Currencies\&call=transfer](https://acala.subscan.io/extrinsic?module=Currencies\&call=transfer)
* 该数据域可以发送网络内任何受支持的token，包括ACA, DOT, LDOT, LCDOT, aUSD等等。

#### currencies.transferNativeCurrency

* [https://acala.subscan.io/extrinsic?module=Currencies\&call=transfer\_native\_currency](https://acala.subscan.io/extrinsic?module=Currencies\&call=transfer\_native\_currency)
* 该数据域可用于发送原生token (ACA). 与currencies.transfer相比，其交易费用要稍微少一些

#### balances.transfer

* [https://acala.subscan.io/extrinsic?module=Balances\&call=transfer](https://acala.subscan.io/extrinsic?module=Balances\&call=transfer)
* 与`currencies.transferNativeCurrency` 相同，只用于原生token (ACA).
* 与 Polkadot兼容 / Polkadot 和其他大多数基于Substrate的链

## 收到Tokens

有很多种方法来监测即将到来的转账：

* 监控事件
* 订阅存储变动消息
* 监控交易

### 监控事件

监控事件是一个值得推荐的方法，可以有效跟踪即将到来的转账。他可以处理**所有**类型的转账交易，甚至可以不是由交易直接发起的转账（比如延迟代理）

#### balances.transfer

* [https://acala.subscan.io/event?module=Balances\&event=Transfer](https://acala.subscan.io/event?module=Balances\&event=Transfer)
* 当原生token ACA转账时发出

#### currencies.transfer

* [https://acala.subscan.io/event?module=Currencies\&event=Transferred](https://acala.subscan.io/event?module=Currencies\&event=Transferred)
* 当一个token发生转账时发出
* 请注意：当使用balances.transfer转账时，不会发出这条消息。

#### currencies.deposit

* [https://acala.subscan.io/event?module=Currencies\&event=Deposited](https://acala.subscan.io/event?module=Currencies\&event=Deposited)
* 当一个token被铸造到一个账户时发出。当是一个跨链转账或者是铸造稳定币的转账时，也有可能发生&#x20;
  * 对于跨链转账，将有 `ExecutedDownward` 事件伴随着存入Token [https://acala.subscan.io/event?address=\&module=dmpqueue\&event=executeddownward](https://acala.subscan.io/event?address=\&module=dmpqueue\&event=executeddownward)

#### xtokens.transferred

* [https://acala.subscan.io/event?address=\&module=xtokens\&event=transferred](https://acala.subscan.io/event?address=\&module=xtokens\&event=transferred)
* 从Acala跨链转账到其他链时发送
* 由 `xtokens.transfer` extrinsic 触发

#### xtokens.transferredmultiasset

* [https://acala.subscan.io/event?address=\&module=xtokens\&event=transferredmultiasset](https://acala.subscan.io/event?address=\&module=xtokens\&event=transferredmultiasset)
* 当发生从Acala到其他链的跨链转账时发出
* 由 `xtokens.transfer_multiasset` extrinsic触发.

### 存储改变RPC

* [state\_subscribeStorage](https://polkadot.js.org/docs/substrate/rpc#subscribestoragekeys-vecstoragekey-storagechangeset)
  * 一系列账户余额数据的订阅。然而，它并不对订阅服务进行保障，因为存在很多连接错误或者区块链重组。

### 监控交易

每个区块取回交易信息，查阅转账交易以及检查转账交易是否成功是可行的。然而，这可能产生假的负面结果，比如收到存款但是未能识别，原因是转账的方式多样。

请参考发送token章节中关于直接转账交易的信息。除了单独发送转账交易之外，还有一些常见的实用方法来批量发送转账交易：

#### utility.batch

* [https://acala.subscan.io/extrinsic?module=Utility\&call=batch](https://acala.subscan.io/extrinsic?module=Utility\&call=batch)
* 这被用于发送打包交易
* 请注意：打包的交易将总是发出成功事件
  * `utility.BatchCompleted` 事件表示所有的交易都已成功
  * `utility.BatchInterrupted` 事件表示交易失败。在失败交易之前的交易被成功执行并且不会被回撤&#x20;

#### utility.batchAll

* [https://acala.subscan.io/extrinsic?module=Utility\&call=batch\_all](https://acala.subscan.io/extrinsic?module=Utility\&call=batch\_all)
* 这与utility.batch相似，但将在交易失败后撤回所有交易
