# 余额类型以及锁仓

## 余额的类型 <a href="#balance-types" id="balance-types"></a>

在 Acala上，有如下几种余额类型：

* **可转账的余额**: 顾名思义，这个余额可以用于转账、支付费用和执行链上的任何行动
* **被锁定的余额:** 该余额是被冻结的。根据计划，他可能被锁定一段时间后才能进行转账，或者它是被锁仓的，也就是每过一段时间一部分token就可以进行转账了。或者是以上两种情况都有。这些tokens的释放是被动地,也就是你需要点击  `claim` 来领取这些token. 下一章将讲述如何领取锁仓的token。
* **总余额:** 是可转账余额和被锁定余额的总和。整个的余额都可以被用于“治理”运营，比如投票。

## 查询&领取锁仓的Token <a href="#check-and-claim-vested-tokens" id="check-and-claim-vested-tokens"></a>

### 通过网页端App来领取锁仓的ACA <a href="#claiming-vested-aca-via-web-app" id="claiming-vested-aca-via-web-app"></a>

你可以在这里领取你的锁仓ACA [https://apps.acala.network/](https://apps.acala.network)​

### 领取锁仓ACA <a href="#claiming-vested-aca" id="claiming-vested-aca"></a>

**尽管一些Token是被锁仓的（或者锁定的），在你将它们转账或者在Acala平台上的Defi应用中使用他们时，你仍然需要先领取这些token。**你可以按照如下指南来学习如何领取你的token：

1\) 前往Polkadot.js **插件** 并且确保其设置成 `allow use on any chain`.

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2F1LjaXAkaK1uXhos9bAs4%2FAllow%20use%20on%20any%20chain.png?alt=media\&token=9c1295d9-4408-4d6a-9b97-47734a9394ee)

2\) 前往[Polkadot JS Apps](https://polkadot.js.org/apps/#/explorer) 并且连接到Acala网络中. 你可以点击左上角的下拉菜单来切换到Acala网络（如下图所示）。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2FQJVMfiWcNZCk3sXU6AFV%2FToggle%20for%20Acala.png?alt=media\&token=39668c28-6a1a-450d-bcab-b95cfff8b4f0)

3\) 选择一个Acala 节点（任何一个都可以）然后点击 `Switch`.

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2FRNZathx5uu6wRSB7G3NG%2FSelect%20Acala.png?alt=media\&token=224536e9-d810-42d4-a1f0-914f08b3b68b)

4\) 选择 `Accounts`. 现在你可以看到你的ACA余额。你可以继续点开你的账户来看有多少是锁仓的（锁定的）。如果有的话，它会在这里显示。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2Fayt60HTQLLGTNkgwUnz3%2Flocked%20tokens%20wiki.png?alt=media\&token=eeac861e-5513-4887-b5c9-c2bdcb63607b)

5\) 前往 `Developer - Extrinsics` , 选择你想领取锁仓token的账户，然后在`submit the following extrinsics`的区域内选择 `vesting` 和 `claim()` ，然后点击`Submit Transaction` 来完成整个过程。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2F4IbCoSH70kW4fnx4Ua3a%2Fclaim.png?alt=media\&token=a0e7747d-23bb-4e74-be82-1485b43bb144)

### 为其他账户领取锁仓的ACA <a href="#claiming-vested-aca-for-other-accounts" id="claiming-vested-aca-for-other-accounts"></a>

用户可以替其他账户领取锁仓的ACA，只需要前往`Developer 中的 Extrinsics` 。选择你希望领取ACA的账户然后通过点击`using the selected account来`启动领取过程. 选择 `vesting` 和`claimFor(dest)`  ，然后选择有锁定token的账户（如截图最下面一栏）。请注意，递交交易只会让锁定的token可以转账，并不会将token转移到发起领取动作的账户中。

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2FLK8HYT57ypCa5IgU99NP%2FScreen%20Shot%202022-01-25%20at%206.53.34%20PM.png?alt=media\&token=db10f90a-0a9d-40a8-ab68-c7f00606e926)

### 检查锁仓状况  <a href="#check-vesting" id="check-vesting"></a>

前往`Developer - Chain state` , 选择 `vesting` 和 `vestingSchedules()` , 然后选择你的账户，点击 `+` 按钮查看锁仓安排。.

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-MAz4EenwXLth\_HO\_hmJ-887967055%2Fuploads%2FqBoHWAkIBOFPrSrm4VtH%2Fvesting%20schedule.png?alt=media\&token=0dd670f4-625e-4c2d-bed0-423fdc9a369a)

如下是一个可能的返回结果示例：

* `start`: token会被锁定，直到 **Polkadot block #**
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
