# 协议信息

## Tokens <a href="#tokens" id="tokens"></a>

* **Acala Token**
  * 名称: Acala
  * 代号: ACA
  * 小数点位: 12
  * 总量: 1,000,000,000
  * Token 类型: 原生 / Tokens(ACA)
  * 查询余额: `system.account`
* **Acala USD**
  * 名称: Acala USD
  * 代号: aUSD
  * 小数点位: 12
  * Token类型: Tokens(AUSD)
  * 查询余额: `tokens.accounts`
  * 总发行量: `tokens.totalIssuance`
* **Liquid DOT:**
  * 名称: Liquid DOT
  * 代号: LDOT
  * 小数点位: 10
  * Token类型: Tokens(LDOT)
  * 查询余额: `tokens.accounts`
  * 总发行量: `tokens.totalIssuance`
* **Liquid Crowdloan DOT**
  * 名称: Liquid Crowdloan DOT
  * 代号: LCDOT
  * 小数点位 10
  * Token 类型: LiquidCrowdloan(13)
  * 查询余额: `tokens.accounts`
  * 总发行量: `tokens.totalIssuance`

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2FSvi2sPsOTBtTRyNdi6Qm%2FScreen%20Shot%202022-02-15%20at%203.22.19%20PM.png?alt=media\&token=3fc719b8-339e-4787-89ca-84f6a22d4348)

## 账户 <a href="#account" id="account"></a>

### 地址格式 <a href="#address-format" id="address-format"></a>

Acala使用 [SS58 (Substrate) address format](https://github.com/paritytech/substrate/wiki/External-Address-Format-\(SS58\)). 相关SS58 信息如下:

* **Acala**: 10 ([ss58 ](https://github.com/paritytech/substrate/blob/df4a58833a650cf37fc97764bf6c9314435e3cb2/ss58-registry.json#L103-L111)注册细节)
* **Karura**: 8 ([ss58 ](https://github.com/paritytech/substrate/blob/df4a58833a650cf37fc97764bf6c9314435e3cb2/ss58-registry.json#L85-L92)注册细节)
* **Mandala**: 42

### 存在性存款 <a href="#existential-deposit" id="existential-deposit"></a>

Acala 使用 [_存在性存款_ (ED)](https://wiki.polkadot.network/docs/learn-accounts#existential-deposit-and-reaping) 来避免太多尘埃账户使得存储的状态数据太过沉重。如果一个账户的存款少于ED, 那么该账户的状态将会从区块链中抹去以保护稀有的链上存储资源。随即该账户余额会被删除并且捐入国库。原生Token ACA的ED在runtime模块中进行配置。非原生token（DOT，aUSD，BTC等）可以通过SKD来链接。ED的数量只能下降，不能上升，所以它尝尝以一个较高的数值开始。在 `pallet_balances` 和 `orml_tokenstransfer` 中的`transfer` 和 `deposit`会检查接收账户的ED。如果账户没有满足ED的要求，转账可能失败。非常典型的案例是你用Token A兑换Token B，如果交易后token A的账户余额小于ED要求，该交易可能失败。一个前端DApp可能会进行检测以避免用户出现这种事故。在[这里](https://github.com/AcalaNetwork/acala-wiki/blob/master/acala/get-started/acala-account/README.md#existential-deposit)阅读更多关于ED的消息

## 协议费用 <a href="#protocol-fees" id="protocol-fees"></a>

* **用DOT & LDOT铸造aUSD：**
  * **清算罚金:** 12%
  * **稳定费:** 3%

## 交易费用 <a href="#transaction-fees" id="transaction-fees"></a>

Acala 采用基于权重的费用，与Gas费不同，这种费用是可预见的并且在调度前收费，[这里](../../ru-men/karura-wang-luo/jiao-yi-fei-yong.md)参阅更多交易费用的信息

## 类型

对于类型的定义可以让SDK知道如何序列化/反序列化区块，交易以及事件。Acala对于类型的定义包可以在[这里](https://unpkg.com/browse/@acala-network/type-definitions@4.0.1/json/typesBundle.json)找到。

## MultiLocation <a href="#multilocation" id="multilocation"></a>

`你可以使用这些`MultiLocation 来添加Acala资产到其他平行链的外部资产列表中：

aUSD:

`{ "parents": 1, "interior": { "X2": [{ "Parachain": 2000 }, { "GeneralKey": [0, 1] } ]}}`

LDOT:

`{ "parents": 1, "interior": { "X2": [{ "Parachain": 2000 }, { "GeneralKey": [0, 3] } ]}}`

ACA:

`{ "parents": 1, "interior": { "X2": [{ "Parachain": 2000 }, { "GeneralKey": [0, 0] } ]}}`

## JS SDK <a href="#js-sdk" id="js-sdk"></a>

Acala.js: [https://github.com/AcalaNetwork/acala.js](https://github.com/AcalaNetwork/acala.js)​

文档: [https://github.com/AcalaNetwork/acala.js/wiki](https://github.com/AcalaNetwork/acala.js/wiki)​

更多参考消息在 [documentation of polkadot.js](https://polkadot.js.org/docs/api/).
