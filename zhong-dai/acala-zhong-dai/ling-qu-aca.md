# 领取ACA

**大多数众贷贡献者不需要进行领取他们ACA或者lcDOT token的操作。他们会自动的打入你账户。**然而，如果你通过https://polkadot.js.org/apps/网站来参与Acala众贷，你需要阅读和同意我们的条款，这样才能领取你的token奖励。

如果你不确定你属于那种方法，你可以前往我们的[分发网站](https://distribution.acala.network) 来了解如何领取你的奖励。你输入你的地址之后，如果你的状态显示为  `To Be Claimed`, 那么你就需要进行领取操作了。

你可以直接进入领取网站 [这里](https://distribution.acala.network/claim/acala).&#x20;

## 选项 1: 使用Polkadot{js} 浏览器扩展程序

前往 [claims website](https://distribution.acala.network/claim/acala). 连接到你的 Polkadot{js} 扩展程序, **使用你参加众贷的账户**, 然后按照弹窗指示来完成流程。

你需要使用扩展程序来对信息签名，该操作并不需要交易费。一旦完成，最多48小时就可以安排分发了。

## 选项 2: 手动领取

前往奖励领取网站.如果你没有通过Polkadot{js}扩展程序参与众贷，你可以选择  `Claim Manually` 并输入你参与Acala众贷的地址。

有两种方法领取奖励：

A) 在Polkadot上发送一个带有特定信息的系统备注，或者

B) 使用**签名和验证**来签署特定的信息 以下是如何使用这两种领取方法的指南。

### A) 使用签名和验证

你可以前往 [Polkadot App - Developer - Sign and Verify](https://polkadot.js.org/apps/#/signing) (Polkadot, Kusama, 或 Acala 都可以). 签名和验证仅仅只是对信息签名，并不需要手续费。

1\) 必须使用用于Acala众贷的账户

2\) 在签署以下数据栏时，请粘贴和复制如下指令来签名（在领取网页显示）

`I hereby agree to the terms of the statement whose SHA-256 multihash is QmeUtSuuMBAKzcfLJB2SnMfQoeifYagyWrrNhucRX1vjA8. (这一段也可以在如下链接中找到:` [`https://acala.network/acala/terms`](https://acala.network/acala/terms)`)`

![](https://lh6.googleusercontent.com/aMJa1Yk5txJJGvhUbsjJ9i87t8WYnAo2m79Te6N4-JYFKpzGAFc8HmQMUZUd1GwxfB0dTw2e7s0195ImUK2Fian40Jkm6ZEaMWaQJvyscOwbtkNrSipTw7nPps39A8n5cbg4WxnU)

3\) 签名，复制哈希然后粘贴回领取网页，即完成流程。

![](https://lh3.googleusercontent.com/ocKhFgo3ZHNnzI0o31FE41g7EPqWyuDvCyp5RtEckeTRcypMhhVQ6wG\_rDNHFo4OIE2QWv2F8BIzux\_XaprEi5DI4t0MtJioC\_Oly9eYKeemQLr1edyd86YxE6uFxOpk8B8p7Pux)

一旦完成手续，最多48小时就会安排分发时间。

### B) 使用系统标记

如果你不能使用**签署和验证**来签署消息，比如你使用了一个代理账户来参与或者你用来参与众贷的机构（比如钱包）没有**签名和验证**设施，那么你可以在Polkadot上发送一个系统备注来领取ACA。

1\) 登录 [Polkadot.js Apps - Polkadot](https://polkadot.js.org/apps/#/explorer), 你必须连接到Polkadot网络中。

2\) 前往Developer-Extrinsics 部分.

![](https://lh4.googleusercontent.com/IJeL--Hr5Zrvho69q2fDJrEu4bQuvQv-VlW4oOUVGQD3dTsmZ0sSFy8nwWnwfofbPH-v\_88pn4COmz4Lg-rDCOlZG8WUa-9FYqSabu\_9Owbn-FOgwtACSQpgRTyUb9NpJMm-vgT-)

3\) **你必须选择与Acala众贷相同账户**。在提交以下extrinsic内容，选择系统，然后在下拉菜单中选择 remarkWithEvent(\_remark)。

![](https://lh4.googleusercontent.com/-z9En1Y8GK4ZCjlt3V5ABDl4EJAhd3lMihjsFUr8SD4lzrUR9qaJOf3p\_xSsd6TZlWKATVPxsaI5UYFmzKusWFW1EgDhycN4b8-F\_C3OcsogRoMMbpqTg3jPflSuXdeQJsRHXSj6)

4\) In the \_remark: Bytes域中, 输入签名所需的消息。复制和粘贴所需的签名信息。（在领取网站上显示）。

`I hereby agree to the terms of the statement whose SHA-256 multihash is QmeUtSuuMBAKzcfLJB2SnMfQoeifYagyWrrNhucRX1vjA8. (也可在如下链接中找到:` [`https://acala.network/acala/terms`](https://acala.network/acala/terms)`)`

点击 `Submit Transaction`. 请注意，你需要支付小额费用来启动交易，所以要确保你的账户有一些资金。

![](https://lh6.googleusercontent.com/tIGP5ZHl8r\_XNT5EKKvylMLWTitl0IAgFoI0IhhNd58WoNzO0m55xcSSd9HCWSiQccHmsLz4ges17a9qC9SgM3diKGgmRw5eno0y271XOvB5lTDy4sF8HXJtYrA9vi5sCZuqg6eh)

5\) 你的标记交易已经递交给Polkadot. 你可以查阅已签名的标记 [Polkadot Subscan Explorer](https://polkadot.subscan.io). 粘贴到Polkadot地址中，用于发送交易

![](https://lh5.googleusercontent.com/17GsCIeXA\_0ijuwCxjuVu3jjRHiSrYaaLMlVY53YkqRpxi6yzTSDP7ASC3BvbAu9ZyWdcxRIQ945fyv0KQK\_aazJ76eZvLqb3\_88hGw6vkL0i\_Ade82Vx100V6TgbewNojuOnKkU)

6\) 你可以在你的交易历史中看到系统消息。点击相应的Extrinsic ID.

7\) 复制`Extrinsic Hash`.

![](https://lh3.googleusercontent.com/w5pF0sy83ZpZ2-CQ\_zO742RD0pqmmSmOI\_1ab1u5ppaCQ05MQSzXVbiHTjsGy3rO1S5TjJE-L7im6dI\_t9qYPy2al9YOh68MZB5cFTSh5xFj3lJR92wA5n0L0LalPXl0Oxca2nH0)

8\) 将 Extrinsic hash 粘贴到 [Claim website](https://distribution.acala.network/claim/acala) 来完成手续。

一旦手续完成，最多48小时就可以安排分发了。
