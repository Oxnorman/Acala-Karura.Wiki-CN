# EVM游乐场

我们已经创建了一个网页应用 - **Acala EVM 游乐场** 来测试Acala EVM的各种功能。这是从Parity的 `canvas-ui`fork出来的。

如想使用游乐场，请前往[https://evm.acala.network](https://evm.acala.network).

在默认的情况下，游乐场是连接到Acala的测试网的。当然也可以连接到本地节点。如果你已经尝试过游乐场，缓存中会有你的连接信息。

## 设置节点连接

请点击游乐场右下角的连接按钮。

![](<../../../../.gitbook/assets/1 (58).png>)

点击 `Node to connect to` 的下拉菜单选择你希望连接的节点：

* 选择 `Local Node` 来连接你本地的Acala节点.
* 选择 `Acala` 来连接已部署的Acala测试网
* 点击 `Use custom endpoint` 来输入自定义的 Websocket URL

![](<../../../../.gitbook/assets/1 (49).png>)

## 查询余额

让我们一起查询一下一个账户的DOT余额。在sidebar左边，点击 `Execute`.

一个原生token合约列表会出现，比如 DOT, aUSD, ACA, renBTC等等。这些原生token（包括跨链资产比如 renBTC）作为预编译的合约开放接入，如不以这种方式，将不能存在于EVM中。他们的供应，账户上的余额和功能都可以在EVM中实现。

选择`DOT` 然后点击 `Execute` 。

![](https://i.imgur.com/gGqwRZM.png)

* 从`Call from Account`选择你的账户 (在例子里就是 `Alice`)&#x20;
* 从`Message to Send`选择 `balanceOf`&#x20;
* 请注意你账户下的 `EVM Address` ， 复制然后粘贴到 `owner: address` 定义区域
* 点击 `Call` 按钮来执行。

![](<../../../../.gitbook/assets/1 (41).png>)

在底栏的 `Call results` 将会显示你账户的DOT余额。

![](<../../../../.gitbook/assets/1 (71).png>)
