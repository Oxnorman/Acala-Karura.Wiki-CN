---
description: RemixRemix
---

# 使用Remix

有很多工具可供你使用来开发和编译Solidity合约，我们展示其中的两个，如下

* online web app Remix&#x20;
* Solidity 开发和测试框架 Waffle

## 使用Remix Comment来编译Solidity合约

本指南介绍了使用 [Remix](http://remix.ethereum.org)创建和部署基于Solidity的智能合约到Acala独立节点的过程。Remix是Ethereum上智能合约常用的开发环境之一。

## **1. 启用 Remix**

前往 [https://remix.ethereum.org/](https://remix.ethereum.org). 在 `Environments`中选择 `Solidity` 来为Solidity的开发配置 Remix , 然后前往 `File Explorers` 查看.

这里有一个使用Remix编译ERC20的例子。打开Remix并且在`File`栏点击 `New File`.&#x20;

![](https://i.imgur.com/J9jtCF4.png)

在右边窗口的文件浏览器中会出现一个输入窗口，你可以在这里输入你的文件名：`BasicToken.sol`.

## **2. 编译Solidity代码**

将如下的代码粘贴到出现的编辑栏

```
pragma solidity ^0.7.0;

import 'https://github.com/OpenZeppelin/openzeppelin-contracts/blob/release-v3.2.0-solc-0.7/contracts/token/ERC20/ERC20.sol';

// This ERC-20 contract mints the specified amount of tokens to the contract creator.
contract BasicToken is ERC20 {
  constructor(uint256 initialSupply) ERC20("BASICT", "BAT") public {
    _mint(msg.sender, initialSupply);
  }
}
```

请注意，这是一个基于开放的Zeppelin ERC-20模板的简单 ERC-20 合约。在建设时，他用代号BAT创建了一个基础的Token, 并且铸造了总的初始供给量

如下是编辑视角：

Remix 将包含所有的Open Zeppelin的依赖都包含进去并编译了合约。

然后在sidebar选择 `Solidity compiler`  然后点击 `Compile BasicToken.sol` 按钮.

Remix 会下载所有的 Open Zeppelin 依赖并且对合约进行编译 。

## **3. 获取 ABI 文件**

前往 `File explorers` , 在`artifacts` 栏里找到 `BasicToken.json` 文件. 粘贴和复制内容并且保存在本地，这就是ABI文件，它可以之后部署到Acala EVM中。

![](<../../../../.gitbook/assets/1 (78).png>)
