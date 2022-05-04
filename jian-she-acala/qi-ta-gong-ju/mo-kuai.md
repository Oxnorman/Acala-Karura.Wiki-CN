# 模块

## Honzon 稳定币模块

### [auction\_manager](https://github.com/AcalaNetwork/Acala/tree/master/modules/auction-manager) 拍卖管理器

`auction_manager` 模块启动和管理各种类型的拍卖--当应计利息超过一定限额时进行盈余拍卖`surplus auction`，当清算头寸的未付债务超过一定限额时进行债务拍卖`debt auction`，以及当头寸被清算时进行抵押品拍卖`collateral auction`。

**盈余拍卖（Surplus Auction）** 当业务正常进行时，通过CDP国库`CDP Treasury`的Honzon协议将从每笔贷款中计提美元的利息。这个盈余将首先覆盖系统中的任何未偿债务。每当这种盈余达到预定的限度，aUSD中的盈余将被拍卖，以换取ACA，然后被烧毁。

**债务拍卖（Debt Auction）** CDP国库`CDP Treasury`也对系统债务进行核算，即核验是否不安全贷款不能完全清偿，是否债务不能完全偿还。如果系统盈余不能覆盖债务，那么债务拍卖`Debt Auction`将被触发，额外的ACA可以被铸造出来拍卖以偿还未偿还的aUSD债务。

**抵押品拍卖（Collateral Auction）** 每笔aUSD贷款的创建都有一个必要的抵押品比率`required collateral ratio`，其抵押品比率需要高于清算比率`liquidation ratio`才能保持安全`safe`。清算比率低于所需的抵押品比率，以便为每笔贷款创造一个安全区，避免在创建时立即清算。如果抵押品的价格下降到一个贷款的抵押比率低于清算比率，那么就会触发抵押品拍卖，以出售抵押品来偿还美元债务。

一般来说，这三种类型的拍卖都遵循类似的格式，除了债务拍卖有一个预设的拍卖结束时间，而其他两种是开放式的：

* 新的出价需要>=旧的出价+目标价格\*最小增量（最小增量为百分比），例如，旧的出价=5美元，目标价格=100美元，最小增量=5%，那么新的出价需要>=10美元
* 如果出价超过目标价格，则开始反向拍卖
* 如果没有新的出价，拍卖将持续到最后的出价时间+AuctionTimeToClose（以区块编号）
* 如果拍卖继续进行，并且超过了AuctionDurationSoftCap（也在区块编号中），那么每个新出价的AuctionTimeToClose将被减半，最小增量加倍，以加快拍卖速度。

### [cdp\_engine](https://github.com/AcalaNetwork/Acala/tree/master/modules/cdp-engine) **cdp引擎**

`cdp_engine` 通过链下工作者管理自动清算和抵押品结算，以及一组风险参数--稳定费、清算比率、清算罚款、所需抵押品比率和最大总借贷价值

每个区块都会收集对aUSD贷款收取的稳定费或利率。拥有的aUSD加上累积的稳定费/利息被记录为借贷单位，每个区块的借贷汇率都会被更新。[`DebitExchangeRateConvertor`](https://github.com/AcalaNetwork/Acala/blob/master/modules/cdp-engine/src/debit\_exchange\_rate\_convertor.rs) 用来计算aUSD的欠款数额。收集的费用被添加到`cdp_treasury`盈余池中。

**`Offchain Worker`** 链下工作者在每个区块结束时运行。 每次只运行一个链下工作者 ，流程是在开始工作前获取一个锁，然后在工作后释放该锁。

* 自动清算：链下工作者将遍历所有贷款，并清算那些不安全的贷款，即当前抵押率低于清算率。它将首先从DeX直接获得aUSD，给与可接受的滑动，否则它将创建抵押品拍卖，以偿还剩余的未偿债务。
* 抵押品结算：在紧急关闭期间，通过收集抵押品到cdp\_treasury来结算所有贷款，并清除债务余额。

### [cdp\_treasury](https://github.com/AcalaNetwork/Acala/tree/master/modules/cdp-treasury)

cdp\_treasury管理着系统全局的`DebitPool`和`SurplusPool`，以及盈余、借贷和抵押品拍卖的参数。&#x20;

在拍卖过程中，一旦有一个被接受的出价，盈余、借方或抵押品的金额就会被转移到cdp\_treasury中。如果有一个新的被接受的出价，那么它将被退还给原来的账户。这确保了系统所需资金的安全。&#x20;

`on_system_surplus` - 当有盈余发生时，例如收取的稳定费用，它将被添加到`cdp_treasury`。这笔盈余将首先用于支付系统债务，但如果它超过了一定的限额，那么将触发盈余拍卖。 on\_system\_debit - 当aUSD贷款被清算时，债务将被添加到cdp\_treasury。



### [honzon](https://github.com/AcalaNetwork/Acala/blob/master/modules/honzon)

honzon是稳定币用户的主要交互点。它提供了以下公共函数。&#x20;

`adjust_loan` - 用它来打开或更新一个aUSD贷款头寸。&#x20;

`transfer_loan_from` - 用它来将给定的aUSD贷款从一个账户转移到另一个账户。

`liquidate_cdp` - 随着链下工作者部署在`cdp_engine`里来自动处理清算cdp，该数值会降低

`settle_cdp`-随着链下工作者部署在`cdp_engine`里来自动处理清算cdp，该数值会降低

### [贷款](https://github.com/AcalaNetwork/Acala/blob/master/modules/loans)

`loans`管理所有抵押品和账户的所有的借方余额和抵押余额。&#x20;

`adjust_position` - 创建或更新aUSD贷款头寸 - 存入/提取抵押品，借入/偿还aUSD，在进行调整之前，它将验证各种条件并检查风险参数。&#x20;

`transfer_loan` - 将一个给定的aUSD贷款的全部余额从一个账户转移到另一个账户。

## [emergency\_shutdown 紧急关停](https://github.com/AcalaNetwork/Acala/tree/master/modules/emergency-shutdown)

`emergency_shutdown` 是风险管理工具之一，特别是作为最后的手段来停止和结算Honzon协议，以保护aUSD和贷款持有人的资产。关闭可以适用于一个或多个抵押资产和相关贷款。

`emergency_shutdown` - 锁定抵押品的价格，停止开放新的贷款，停止所有的拍卖，结算未偿贷款，将剩余的抵押品归还给所有者。

注意：一个抵押资产可以单独关闭，不是通过 `emergency_shutdown` 模块，而是通过在 `cdp_engine` 模块中设置 `set_global_params`，来限制最大总债务值（债务上限），以停止新贷款的开启，并逐步提高清算比率，以解决未偿贷款。

## 去中心化交易所

\[TODO]

## 总体

### [currencies](https://github.com/AcalaNetwork/Acala/tree/master/modules/currencies) 货币

Acala网络是一个多种token网络。原生网络token又名ACA，由`balances` Pallet管理。所有其他token都由 [`tokens` 模块](https://github.com/laminar-protocol/open-runtime-module-library/tree/master/tokens)管理。[`currency` 模块](https://github.com/laminar-protocol/open-runtime-module-library/tree/master/currencies)通过结合两者实现对多token的支持。&#x20;

`accounts` 处理特殊的转账，例如在给定条件下的免费转账，例如，当一定数量的原生token ACA被存入并锁定，那么一定数量的免费转账交易将被启用。

### 空投

待完成

### [产品基础组件](https://github.com/AcalaNetwork/Acala/tree/master/modules/primitives)

`CurrencyId` 列出网络上所有支持的Token。`AirDropCurrencyId`列出空投token，这在Mandala网络上可用来记录金丝雀网络和主网token空投余额。一旦这两个后来的网络启动，它将被用于token认领。
