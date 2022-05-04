# 部署合约

`Acala EVM Playground` 对于测试Acala EVM的各种功能非常有用。他是从Parity的 `canvas-ui`分叉而来。

## **1. 设置**

为了部署你的智能合约，你可以用我们的测试网或者运行你的本地开发节点。

### 运行你的开发节点\*\*

要运行你的开发节点，你可以。1. 在本地建立Acala项目。你可以按照这里的指南来做：[https://github.com/AcalaNetwork/Acala#3-building](https://github.com/AcalaNetwork/Acala#3-building)。一旦你建立了Acala，你可以通过运行以下命令来启动一个已准备好的EVM本地开发节点。

```
make run-eth;
```

1. 使用预先构建的Acala Docker镜像

你需要在你的机器上安装Docker，你可以按照这里的安装说明。安装 [Docker](https://docs.docker.com/get-docker/)。一旦Docker运行，你需要拉出最后一个acala镜像并运行它：

```
docker pull acala/acala-node:latest
docker run -p 9944:9944 acala/acala-node:latest --name "calling_home_from_a_docker_container" --rpc-external --ws-external --rpc-cors=all --dev
```

一旦你的节点正在运行，你应该可以在终端窗口看到如下类似的显示:

![](<../../../../.gitbook/assets/1 (65).png>)

在你的开发节点建立和运行后，你可以通过点击左下角的下拉菜单，选择`Local Node`，将Acala EVM游乐场指向你的节点。

![](<../../../../.gitbook/assets/1 (40).png>)

运行本地开发节点将用预支付的开发者账户预填充`Accounts`&#x20;

#### 部署到我们的测试网络&#x20;

要部署到我们的测试网络，你需要在浏览器中安装polkadot{.js}钱包扩展程序。&#x20;

一旦你安装了该扩展，你可以用EVM地址绑定你的账户，并在Acala EVM游乐场的设置EVM账户页面上获得测试网络资金。如需更深入的说明，请阅读这里的[文档](she-zhi-evm-zhang-hu.md)。&#x20;

注意：在本页面的其余部分，我们将假设你使用的是一个本地开发节点。如果你使用polkadot{.js}扩展部署到测试网络，只需将Alice和Bob的账户替换为你在扩展中设置的账户。

## 2. 上传合约的ABI和字节码

前往 [https://evm.acala.network](https://evm.acala.network)，上传`BasicToken` 的ABI和字节码文件。

前往上传页面。

![](<../../../../.gitbook/assets/1 (18).png>)

填上合约名称，然后上传合约文件`BasicToken.json`。

![](<../../../../.gitbook/assets/1 (13).png>)

它会展示在合约中可用方法的列表。然后点击上传。

## **3. 部署合约**

在上传完ABI和字节码文件之后，游乐场会自动前往部署页面。如果没有的话，请在左边的Sidebar中手动选择。 `BasicToken` 会出现在 `ABI bundles`.

点击`Deploy` 按钮，然后选择 `Alice` (或者如果使用浏览器插件的话，请选择你自己的账户）作为部署账户。

![](<../../../../.gitbook/assets/1 (12).png>)

设置初始值（比如`1000`）然后点击部署。

![](<../../../../.gitbook/assets/1 (22).png>)

在确认交易之后，你会被自动跳转到执行页面。或者你可以手动前往，点击左边sidebar的执行。

![](<../../../../.gitbook/assets/1 (8).png>)

## **4. 与合约互动**

前往执行页面，找到部署的 `BasicToken` 合约然后点击 `Execute` 按钮，该按钮在 "BasicToken" 框的下面.

## **5. 查询余额**

为了查询账户余额，你按照如下操作:

1. 从`Call from Account`下拉菜单中选择 `Alice` 。这是用来发送交易的账户
2. 在`Message to Send`下拉菜单中选择 `balanceOf`
3. 在`Call from Account`找到Alice的EVM地址，复制和粘贴到输入框中 `: address` input.

![](https://i.imgur.com/xH1j0ph.png)

**注意:** Solidity合约一般有两种方式: `views` 和 `executable` 方式.

* `Views` 是用于查询链上信息，但不需要向链上写入信息。`Views` 交易是免费的。游乐场使用  `Call` 按钮来声明他 to indicate this.
* `Executable` 方法可以写数据到链上，这些交易不是免费的。点击`Execute` 按钮来执行。

最后点击底部的 `Call` ，并且 `Call results` 会展示Alice的BasicToken余额 (1000)

![](<../../../../.gitbook/assets/1 (10).png>)

## 6. 转账&#x20;

现在，让我们尝试将BasicTokens转账到Bob的账户。&#x20;

1. 从账户下拉菜单中选择Alice。&#x20;
2. 从`Message to Send`下拉菜单中选择`Transfer`。&#x20;
3. 从`Call from Account`下拉菜单中选择Bob的账户（别忘了像我们为Alice做的那样把EVM地址绑定到BOB的账户上），然后复制它的EVM地址并粘贴到收件人地址输入框。(记得将`Call from Account`切换回Alice)&#x20;
4. 在`amount: unit256`参数框中输入转账金额，注意Token有一个标准的18位小数。 单击 "执行"。

![](<../../../../.gitbook/assets/1 (21).png>)

一个弹窗通知会确认交易已经成功。

现在检查Alice和Bob的余额，然后确认数据已经改变。Alice的账户如下：

![](<../../../../.gitbook/assets/1 (3).png>)

Bob的账户如下：

![](<../../../../.gitbook/assets/1 (9).png>)
