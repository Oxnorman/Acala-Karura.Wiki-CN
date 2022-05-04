# 余额类型以及兑付

## 余额的类型 <a href="#balance-types" id="balance-types"></a>

在 Acala上，有如下几种余额类型：

* **可转账的余额**: 顾名思义，这个余额可以用于转账、支付费用和执行链上的任何行动
* **被锁定的余额:** 该余额是被冻结的。根据计划，他可能被锁定一段时间后才能进行转账，或者它是被锁仓的，也就是每过一段时间一部分token就可以进行转账了。或者是以上两种情况都有。这些tokens的释放是被动地,也就是你需要点击  `claim` 来领取这些token. 下一章将讲述如何领取锁仓的token。
* **总余额:** 是可转账余额和被锁定余额的总和。整个的余额都可以被用于“治理”运营，比如投票。

## 查询&领取锁仓的Token <a href="#check-and-claim-vested-tokens" id="check-and-claim-vested-tokens"></a>

### 通过网页端App来领取锁仓的KAR <a href="#claiming-vested-aca-via-web-app" id="claiming-vested-aca-via-web-app"></a>

你可以在这里领取你的锁仓ACA [https://apps.karura.network/portfolio](https://apps.karura.network/portfolio)​

### 在Polkadot App中 <a href="#claiming-vested-aca" id="claiming-vested-aca"></a>

前往 [Polkadot App - Karura Parachain - Accounts section](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkarura-rpc-1.aca-api.network#/accounts), 查询账户余额。如果有锁仓（锁定的）余额，将在这里显示。

![](<../../../.gitbook/assets/1 (37).png>)

前往 `Developer - Extrinsics` , 选择你想领取锁仓token的账户，然后在`submit the following extrinsics`的区域内选择 `vesting` 和 `claim()` ，然后点击`Submit Transaction` 来完成整个过程。

![](<../../../.gitbook/assets/1 (28).png>)

### 检查锁仓状况  <a href="#check-vesting" id="check-vesting"></a>

前往`Developer - Chain state` , 选择 `vesting` 和 `vestingSchedules()` , 然后选择你的账户，点击 `+` 按钮查看锁仓安排。.

![](<../../../.gitbook/assets/1 (5).png>)

如下是一个可能的返回结果示例：

* `start`: token会被锁定，直到 **Kusama block #**
* `period`: 释放周期 比如，每个区块释放一次或者每432,000区块释放一次&#x20;
* `periodCount`: 多少个锁仓周期
* `perPeriod`: 每个周期释放多少数量的token

```
[
  {
    start: 13,795,200
    period: 432,000
    periodCount: 12
    perPeriod: 100 ACA
  }
]
```

### 在Karura App上

你可以领取锁仓KAR中已经释放的部分，请前往 [Karura App](https://apps.karura.network).

![](<../../../.gitbook/assets/1 (52).png>)



### &#x20;<a href="#check-vesting" id="check-vesting"></a>

