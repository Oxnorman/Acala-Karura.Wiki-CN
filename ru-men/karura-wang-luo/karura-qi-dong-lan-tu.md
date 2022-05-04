# Karura启动蓝图

Karura网络采用阶段性启动计划 。请查看[实时动态路线图 ](https://www.notion.so/dcabf9ba7c6246c69b913d5972503227?v=4121894373fd43d98ffcac260803928d)来及时了解当前的计划。.

**当前阶段: 技术验证 & Runtime升级**

## 🚀 (已完成) Karura 创世 - 启动

Karura网络的创世区块将以PoA网络在2021年6月23号正式启动。治理权限由一个超级用户（sudo）钥匙控制，该钥匙由Acala基金会保管，主要任务为执行交易，开启升级来决问题以及完成启动过程。&#x20;

自创世以来，Karura网络安全由Polkadot的NPoS的验证人来保证。在当前这个阶段，Karura收集人是由节点服务合作伙伴组成。

**Karura 平行链信息可以在** [**Subscan**](https://acala.subscan.io) **&** [**Polkadot App**](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Facala.api.onfinality.io%2Fpublic-ws#/explorer) **上查询到。**

## 🏒 (已完成) **完成KAR分发**

**查询 KAR分发**[**这里**](https://distribution.acala.network)**.**

* [x] 测试网宣传奖励以及空投
* [x] "建设 Acala #1" 奖励
* [x] Karura 众贷
* [x] 其他事件

## 🕵️ (已完成) 技术验证 & Runtime升级&#x20;

Karura 将进行一系列的测试和验证来确保网络可以正常运行

* [x] 收集人如期产出区块
* [x] Kusama 按预期验证来自Acala的区块
* [x] Runtime 升级来修复错误
* [x] Block时间趋于稳定
* [x] p2p连接正常
* [x] RPC节点可用

## 🤹 (完成) 启用从Kusama到Karura的KSM转账&#x20;

从Kusama中继链通过**xtoken**转账KSM到Karura平行链，以及反向转账。然而，在Karura平行链之间的转账在当前阶段还无法实现。

了解详细内容请点击[这里](karura-de-nei-bu-zhuan-zhang.md)。

## 🎯 (完成) 分发KAR

打包分发KAR到

* [x] 测试网宣传奖励和空投
* [x] ”建设Acala #1“计划的参与者&#x20;
* [x] Karura众贷参与者
* [x] 其他事件

如果你通过交易所或者托管中介参与众贷，你的奖励将通过这些交易所和托管机构发放给你。请直接与他们联系来确认分发安排。

## 🎁 (完成) 领取KAR

**你可以在**[**这里**](../../zhong-dai/karura-zhong-dai/ling-qu-kar.md)**查询你的KAR奖励是否需要提取。**

如果你通过交易所或者托管中介参与众贷，你的奖励将通过这些交易所和托管机构发放给你。请直接与他们联系来确认分发安排。.

如果你是通过Polkadot 网页端应用直接参与Karura的众贷，或者通过非托管钱包（非Polkawallet和fearless钱包），在你取回你的Karura奖励之前，你需要先同意我们的条款。取回你Karura奖励的网页在[这里](https://distribution.acala.network/claim).

## ✋ (完成) 理事会治理 + 民主

在与收集者合作使得链运行稳定的情况下，sudo钥匙会进行runtime升级并启用任命的理事会议员和民主。其他理事会包括金融理事会，技术理事会，流动性质押理事会以及民意公投都将启动。

更多信息请点击 [这里](https://github.com/AcalaNetwork/acala-wiki/blob/master/acala/get-started/governance/participate-in-democracy.md).

## 💥 (完成) 移除 Sudo

Sudo模块将通过runtime升级来移除，并且Acala网络之后将由链上治理和token的持有者共同治理。

阅读更多信息请点击 [这里](https://acala.discourse.group/t/1-acala-runtime-upgrade-disable-sudo-enable-token-transfers/163).

## 🚃 (完成) 开启转账

从此Karura网络内部转账将不受限制

## 👩‍🌾 (进行中) 核心的DeFi功能

随着我们启动每一条Defi协议，更多信息会提供在这里。

* [x] Karura DeX
  * [x] 开启 DeX
  * [x] 开启 KSM/KAR 交易对
    * [x] 开始 Bootstrap
    * [x] 交易启动
  * [x] KSM/kUSD交易对
    * [x] 开始Bootstrap
    * [x] 交易启动
    * [x] 开始流动性计划
  * [x] KAR/kUSD 交易对
  * [x] LKSM/kUSD交易对
  * [x] ...
* [x] kUSD Borrowing
  * [x] 开启 kUSD 稳定币协议
  * [x] 开启 KSM 抵押 (有上限)
  * [x] 开启 LKSM 抵押
  * [x] ...
* [x] Liquid KSM
  * [x] 开启 "Canary" 流动性 KSM
    * [x] 铸造 LKSM - 只有当网络升级到去信任的流动性质押，提取LKSM才可用
    * [x] KSM 质押奖励产生&#x20;
    * [x] LKSM 作为抵押品
  * [x] 流动性质押升级
* [ ] USDT
  * [ ] 作为抵押物
  * [ ] 作为交易对
* [x] 启动 Acala EVM
