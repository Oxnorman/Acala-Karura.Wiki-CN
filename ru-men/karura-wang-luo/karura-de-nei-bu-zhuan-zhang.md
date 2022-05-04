# Karura的内部转账

Karura是一个实验性网络，或者叫做Acala的“金丝雀网络”。他是Acala代码的早未审计版，但也有自己真实的经济价值。本质上他是高度试验性的。

⚠️  交易所当前不会支持直接从Karura网络上提取/存入KSM。**请不要在发送KSM到交易所在Karura App上的地址。**阅读更多请点击[这里](qian-bao-zhang-hu/jiao-yi-suo-de-cun-qu-token.md)。

* [Karura Web App转账指南](https://app.gitbook.com/s/KeTDqHyNU6y7YYEquKWV/kai-shi-shi-yong-karura/zhuan-zhang-zhi-nan)

## 为什么转账KSM到Karura

KSM是Kusama上的原生token。他被用作手续费token，质押token以及在Kusama中继链上用作网络安全和治理token等。 Karura平行链的启动为KSM带来全新的应用场景:

* 通过[Karura Swap](karura-de-nei-bu-zhuan-zhang.md)来参与与其他token的去信任交易
* 在Karura Swap中，使用KSM为基于KSM的交易对提供流动性。比如KAR/KSM交易对（在[这里](karura-de-nei-bu-zhuan-zhang.md)学习更多关于成为流动性提供商&相关风险）。
* 使用KSM来作为抵押品铸造aUSD稳定币，aUSD稳定币为交易加杠杆或者其他应用场景
* 可以质押到Karura的流动性KSM质押池中来铸造LKSM（将LKSM作为抵押品），或者转账和交易。
  * LKSM 是一个可编程的质押资产，是需要其他协议和应用构建的基础

## 跨链同质化token的转账

使用Polkadot的 [Cross-chain Message Passing (XCMP)](https://wiki.polkadot.network/docs/learn-crosschain) 技术进行跨链转账, 具体来说就是用 [Horizontal Relay-routed Message Passing (HRMP)](https://wiki.polkadot.network/docs/learn-crosschain#horizontal-relay-routed-message-passing-hrmp) 作为发送和接受通用跨链信息的基础。对于发送和接受同质化token，Karura使用由Acala开发的xtoken同质化token来实现转账功能。&#x20;

你可以在这里找到源代码: [xtokens](https://github.com/open-web3-stack/open-runtime-module-library/tree/3bf16d6efc8c35039a062748ff20fa6db6e8faa0/xtokens) 和 [xcm-support](https://github.com/open-web3-stack/open-runtime-module-library/tree/3bf16d6efc8c35039a062748ff20fa6db6e8faa0/xcm-support).&#x20;

你可以在[这里](https://github.com/paritytech/xcm-format)找到由Parity团队开发的跨链信息格式（XCM）。

## 从Kusama转账KSM到Karura

使用 [Karura App](https://apps.karura.network/portfolio), 前往 `Cross Chain` 然后选择`Inter Kusama Transfer`.&#x20;

**注意:** 你登录Karura app里面的账户必须要有一定数量的KSM（也请注意存在性存款的要求）

从 `From Chain`选择 `Kusama` , 和从 `To Chain` 中选择`Karura` 。 你KSM余额(在Kusama上) 会在这里显示. 然后选择 `To Account`, 这个就是你想通过此账户进入Karura app的账户。

![](<../../.gitbook/assets/1 (63).png>)

交易费用可分为两个部分 (在[这里](jiao-yi-fei-yong.md)阅读更多关于费用的消息)

* &#x20;`Origin Chain Transfer Fee` 由 Kusama收取
* &#x20;`Destination Chain Transfer Fee` 由Karura收取,  Statemine链很相似

然后点击 \`Transfer\`, 请保持耐心，对于Kusama中继链来说，可能需要一些时间来发送和确认你的KSM已经发送到Karura 🚀。

![](<../../.gitbook/assets/1 (35).png>)

**在Karura这边**

Subquery 的部署江会让搜索更加方便以及更容易找到你的跨链交易。现在你可以前往Karura的Subscan开始搜索 `module = parachainsystem` 和 `event = downwardmessagesprocessed`. 或 [使用这个链接](https://karura.subscan.io/event?address=\&module=parachainsystem\&event=downwardmessagesprocessed\&startDate=\&endDate=) 导航到目的地。

[Subscan上的交易示例](https://karura.subscan.io/extrinsic/135672-1?event=135672-1)

## 从Karura上转账KSM到Kusama

使用 [Karura App](https://apps.karura.network/portfolio), 前往 `Cross Chain` 然后选择 `Inter Kusama Transfer`.&#x20;

&#x20;在`From Chain`中选择 `Karura` 和在 `To Chain` 中选择`Kusama` 。你的KSM余额（在Karura上）就显示出来. T然后选择 `To Account`，该账户为你登录Karura app时想用的账户。请确保你账户在 Polkadot{js}扩展程序中已经设置成 `Allow use on any chain`&#x20;

![](<../../.gitbook/assets/1 (68).png>)

交易费用可分为两个部分 (在[这里](jiao-yi-fei-yong.md)阅读更多关于费用的信息)

* &#x20;`Origin Chain Transfer Fee` 由 Karura收取
* &#x20;`Destination Chain Transfer Fee` 由Kusama收取

然后点击 \`Transfer\`, 请保持耐心，可能需要一点时间让你的KSM返回到Kusama上 🚀

### 检查交易

这里面包含两个交易，一个是发生在Karura上，发送KSM到Kusama中继链上；第二个是发生在Kusama上，发送KSM到指定的账户。

**在Karura这边**

Subquery 的部署江会让搜索更加方便以及更容易找到你的跨链交易。现在你可以前往[Karura Subscan Explorer](https://karura.subscan.io)开始搜索 `module = xtoken`和`account = sender account`. 或 [使用这个链接](https://karura.subscan.io/event?address=\&module=parachainsystem\&event=downwardmessagesprocessed\&startDate=\&endDate=) 导航到目的地。

[Subscan上的交易示例](https://karura.subscan.io/extrinsic/135672-1?event=135672-1)

**在Kusama这边**

前往 [Kusama Subscan Explorer](https://kusama.subscan.io), 搜索你的Kusama账户, 你会在Extrinsics列表里看到相关的 `xcmpallet` 交易。

[Subscan上的交易示例](https://kusama.subscan.io/extrinsic/8338413-2)
