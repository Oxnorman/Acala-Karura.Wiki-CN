# 设置EVM账户

## 单一钱包，单一账户的体验&#x20;

用户可以使用**一个扩展/钱包**和**一个单一的Substrate账户**与Substrate的runtime、EVM中的合约和wasm合约或这些的混合体进行互动。如果用户想使用一个特定的以太坊地址，那么只需将其与他/她的Substrate地址联系起来（基本上证明用户拥有这两个地址），此后用户只需使用Polkadot{js}扩展或类似的Substrate账户，就可以无缝地签署任何以太坊交易。&#x20;

这使得用户可以使用Acala内的所有功能和跨链能力，而无需管理多个账户或钱包。&#x20;

## 设置EVM账户&#x20;

Acala上的用户将始终拥有一个基于Substrate的账户，使用户能够轻松浏览多个区块链，并通过一个账户签署任何（EVM和Susbtrate）交易。按照[这里](https://wiki.polkadot.network/docs/learn-account-generation)的指南来生成一个Substrate账户。&#x20;

要启用单一账户并使用Acala EVM，你必须&#x20;

1. 绑定一个自动生成的以太坊地址或&#x20;
2. 将一个现有的以太坊账户绑定到基体账户上

### 1. 绑定一个自动生成的EVM账户&#x20;

用户可以为每个Substrate账户生成一个EVM地址。然后，用户可以将EVM地址与Substrate账户绑定，因此Substrate账户上的原生Token余额，如DOT、renBTC、aUSD等，都可以在EVM地址上使用。&#x20;

在Acala EVM中，如果资金被发送到没有相关EVM地址的底层账户，将自动生成一个EVM地址并与底层账户绑定。&#x20;

Substrate账户和相关EVM地址之间的余额会自动同步。例如，一个用户将10个RenBTC转账到Acala，他/她的余额将显示在Substrate账户中，该余额也将显示在EVM地址中并可以转移。&#x20;

#### EVM地址的生成&#x20;

EVM地址是使用`blake2_256`哈希函数生成的，前缀为evm，相关的Substrate账户作为输入。请看[这里](https://github.com/AcalaNetwork/Acala/blob/master/modules/evm-accounts/src/lib.rs#L185-L186)的源代码。&#x20;

```
blake2_256("evm:" ++ account_id)[0..20]
```

#### 通过EVM游乐场生成EVM地址

导航到[EVM游乐场](https://evm.acala.network/#/evmAccount)（ 一个网页应用来测试各种Acala EVM功能）。

如果你还没有准备好，请导航到`Setup EVM Account`

![](<../../../../.gitbook/assets/1 (69).png>)

#### 步骤1： 选择一个Substrate账户

如果你还没有安装 Polkadot{js}扩展程序和创建一个账号，请按照[这里](https://wiki.polkadot.network/docs/learn-account-generation)的步骤来实现。

如果账户已经创并且扩展程序已经正确安装，账户在下拉菜单中就应该已经可见了。

点击`Faucet`键来给账户充币，由于他需要发送一笔交易到Acala区块链是那个来连接账户。

![](<../../../../.gitbook/assets/1 (15).png>)

**步骤2：选择选项1来绑定一个自动生成EVM地址**

**步骤3：绑定**

在步骤3中你可以看到一个已经生成的EVM地址，然后点击`bind`。

Polkadot{js}扩展程序将提示你输入密码或者用之前存储的密码，然后点击`Sign the transaction`。

![](<../../../../.gitbook/assets/1 (39).png>)

如果绑定交易成功，你会收到`An evm account already exists to bind this account`  这条信息，基本意味着绑定已经记录在链上，你可以对任何EVM交易使用Polkadot扩展程序了。

![](<../../../../.gitbook/assets/1 (16).png>)

### 2. 绑定现有的Ethereum账户&#x20;

在任何情况下，如果用户想在Acala EVM中使用现有的以太坊账户，这个地址将需要被认领并绑定到他们的Subatrate账户。&#x20;

**一个Substrate账户只能与一个Ethereum地址关联**。已经链接到生成的EVM地址的Substrate地址不能再链接到现有的Ethereum地址，反之亦然。&#x20;

绑定一个现有的以太坊账户需要用户证明他们拥有以太坊账户的私钥，通过签署一个消息，将其包含在一个`claim`交易中并将其发送到Acala网络。&#x20;

**第一步：获取创世的哈希值**&#x20;

1. 从[Polkadot应用程序](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmandala-tc7-rpcnode.aca-dev.network%2Fws#/settings/metadata)的**设置**部分选择**元数据**
2. 复制**创世哈希**的十六进制字符串

![第一步：获取创世的哈希值](<../../../../.gitbook/assets/1 (38).png>)

#### 第2步：为你的目标地址获取链ID&#x20;

* 选择 "**开发者** "选项卡，然后从下拉菜单中选择**链状态**&#x20;
* 选择**常量**，然后从**常量查询**下拉菜单中选择**evm**&#x20;
* 从方法/动作下拉菜单中选择**chainId**&#x20;
* 点击右边的 "+"按钮

![开发者>链状态>常数>EVM>链ID](<../../../../.gitbook/assets/1 (79).png>)

#### 第3步：在[EVM+](https://evm.acala.network/#/Bind%20Account)游乐场创建”领取“的签名&#x20;

1. 在Metamask中选择合适的账户&#x20;
2. 填写**Substrate地址**、**链ID**和**创世哈希值**&#x20;
3. 点击**签名**并将**签名**复制到下一个步骤

![步骤3：创建”领取“的签名](<../../../../.gitbook/assets/1 (4).png>)

#### 第4步：在[Polkadot应用程序](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fmandala-tc7-rpcnode.aca-dev.network%2Fws#/extrinsics)的开发者选项中领取账户

**ethAddress**应该与你上面用来生成签名的Metamask钱包地址相同。&#x20;

1. 从**extrinsic**菜单中选择**evmAcounts**&#x20;
2. 从方法/行动下拉菜单中选择 **claimAccount(ethAddress, ethSignature)**&#x20;
3. 填入**ethAddress**和**ethSignature**&#x20;
4. 点击**提交交易**

![步骤4：填入eth地址和eth签名](<../../../../.gitbook/assets/1 (7).png>)

第5步：确认捆绑&#x20;

1. 选择 "**Develper** "选项，然后从下拉菜单中选择**Chain state**&#x20;
2. 选择**存储**，然后从**状态查询**的下拉菜单中选择**evmAccounts**&#x20;
3. 点击右边的 "+"按钮&#x20;
4. 仔细检查**evmAccounts.evmAddresses**是否确实是正确的

![开发者>链状态>存储>evm账户>evm ](<../../../../.gitbook/assets/1 (76).png>)

#### 使用案例&#x20;

下面是绑定现有Ethereum地址的两个潜在用例。&#x20;

#### 案例1&#x20;

例如，Ethereum上的一个DeFi协议现在正通过在Acala网络上部署他们的合约，将其业务扩展到Polkadot。他们将这个新的分支通过空投代币给他们现有的用户，如果他们也使用Acala上的协议。 最简单的方法是将代币空投到Acala上现有的以太坊地址。因此，用户只需将他们当前的以太坊地址绑定到一个Substrate地址，将其用于任何EVM交易，并接收空投。&#x20;

**案例2**&#x20;

对于像[Linkdrop](https://linkdrop.io)这样的DApps，用户需要使用Ethereum私钥来签署信息。在Acala上使用Linkdrop，将需要用户申请他们现有的以太坊地址，并将其绑定到他们的Substrate账户。此后，他们可以代表以太坊账户发送交易。
