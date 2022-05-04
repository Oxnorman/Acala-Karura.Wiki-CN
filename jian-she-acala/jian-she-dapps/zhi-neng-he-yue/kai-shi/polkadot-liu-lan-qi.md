# Polkadot 浏览器

Polkadot浏览器用于与Acala节点进行通信，可以查询区块链的状态，例如账户余额、区块信息等。还可以执行交易与链上的各种Runtime模块进行互动，例如转移Token，在DeX上进行代币交换等。&#x20;

打开[Polkadot浏览器](https://polkadot.js.org/apps/#/)。&#x20;

控制台是由Polkadot提供的一个前端，可以连接到各种Substrate节点。要将控制台连接到你的特定节点，打开左上角的下拉菜单

![](<../../../../.gitbook/assets/1 (44).png>)

打开`Development`部分，选择`local node` 来连接到你的本地Acala节点。

![](<../../../../.gitbook/assets/1 (29).png>)

选择`custom` 连接到已部署的节点，并将Websocket URL粘贴到`custom endpoint` 输入框中。&#x20;

然后点击顶部的`Switch`，等待页面刷新并连接到网络。如果你当前的端点已经符合你的选择，`Switch` 按钮将被禁用。&#x20;

## 查询余额&#x20;

点击顶部导航栏上的 `Developer` 标签，在下拉列表中选择 "Chain State"。

![](<../../../../.gitbook/assets/1 (23).png>)

如果想进行状态查询和获取你账户的余额信息，请按照如下操作：

1. 点击 `selected state query`, 然后选择 `tokens`.
2. 选择 `accounts` 存储.
3. 从`AccountId` 的下拉菜单中选择你的账户（在例子中就是 `Alice` )&#x20;
4. 从`CurrencyId`下拉菜单中选择 `Token`, 以 `DOT` 作为 `Token: TokenSymbol`
5. 点击 `+` 按钮来发起调用

![](<../../../../.gitbook/assets/1 (53).png>)

你的账户余额将展示如下：

![](<../../../../.gitbook/assets/1 (43).png>)
