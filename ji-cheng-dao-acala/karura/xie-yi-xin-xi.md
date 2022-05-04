# 协议信息

## Tokens <a href="#tokens" id="tokens"></a>

* **Token 小数位数:**
  * Karura (KAR): 12
  * LKSM: 12
  * Karura Dollar (kUSD): 12
* **基本单位:** “Plank"
* **余额类型:**
* **总固定供给量 KAR:** 100,000,000

## 账户 <a href="#account" id="account"></a>

### 地址格式 <a href="#address-format" id="address-format"></a>

Karura使用 [SS58 (Substrate)地址格式](https://github.com/paritytech/substrate/wiki/External-Address-Format-\(SS58\)) 。相关SS58 信息如下:

* **Acala**: 10 ([ss58 ](https://github.com/paritytech/substrate/blob/df4a58833a650cf37fc97764bf6c9314435e3cb2/ss58-registry.json#L103-L111)注册细节)
* **Karura**: 8 ([ss58 ](https://github.com/paritytech/substrate/blob/df4a58833a650cf37fc97764bf6c9314435e3cb2/ss58-registry.json#L85-L92)注册细节)
* **Mandala**: 42

### 存在性存款 <a href="#existential-deposit" id="existential-deposit"></a>

Karura使用 [_存在性存款_ (ED)](https://wiki.polkadot.network/docs/learn-accounts#existential-deposit-and-reaping) 来避免太多尘埃账户使得存储的状态数据太过沉重。如果一个账户的存款少于ED, 那么该账户的状态将会从区块链中抹去以保护稀有的链上存储资源。随即该账户余额会被删除并且捐入国库。原生Token KAR的ED在runtime模块中进行配置。非原生token（KSM，aUSD，BTC等）可以通过SKD来链接。ED的数量只能下降，不能上升，所以它尝尝以一个较高的数值开始。在 `pallet_balances` 和 `orml_tokenstransfer` 中的`transfer` 和 `deposit`会检查接收账户的ED。如果账户没有满足ED的要求，转账可能失败。非常典型的案例是你用Token A兑换Token B，如果交易后token A的账户余额小于ED要求，该交易可能失败。一个前端DApp可能会进行检测以避免用户出现这种事故。在[这里](https://github.com/AcalaNetwork/acala-wiki/blob/master/acala/get-started/acala-account/README.md#existential-deposit)阅读更多关于ED的消息

## 协议费用 <a href="#protocol-fees" id="protocol-fees"></a>

* **用KSM\&LKSM来铸造aUSD:**
  * **清算罚金:** 12%
  * **稳定费:** 3%

## 交易费用 <a href="#transaction-fees" id="transaction-fees"></a>

Karura 采用基于权重的费用，与Gas费不同，这种费用是可预见的并且在调度前收费，[这里](../../ru-men/karura-wang-luo/jiao-yi-fei-yong.md)参阅更多交易费用的信息

## 类型

对于类型的定义可以让SDK知道如何序列化/反序列化区块，交易以及事件。Karura对于类型的定义包可以在[这里](https://unpkg.com/browse/@acala-network/type-definitions@4.0.1/json/typesBundle.json)找到。

## MultiLocation <a href="#multilocation" id="multilocation"></a>

`你可以使用这些`MultiLocation 来添加Karura资产到其他平行链的外部资产列表中：

aUSD:

`{ "parents": 1, "interior": { "X2": [{ "Parachain": 2000 }, { "GeneralKey": [0, 129] } ]}}`

LKSM:

`{ "parents": 1, "interior": { "X2": [{ "Parachain": 2000 }, { "GeneralKey": [0, 131] } ]}}`

KAR:

`{ "parents": 1, "interior": { "X2": [{ "Parachain": 2000 }, { "GeneralKey": [0, 128] } ]}}`

## JS SDK <a href="#js-sdk" id="js-sdk"></a>

Acala.js: [https://github.com/AcalaNetwork/acala.js](https://github.com/AcalaNetwork/acala.js)​

文档: [https://github.com/AcalaNetwork/acala.js/wiki](https://github.com/AcalaNetwork/acala.js/wiki)​

更多参考消息在 [documentation of polkadot.js](https://polkadot.js.org/docs/api/).
