# 使用Waffle

有很多工具可供你使用来开发和编译Solidity合约，我们展示其中的两个，如下

* online web app Remix&#x20;
* Solidity 开发和测试框架 Waffle

## 使用Waffle Comment来编译Solidity合约

**请注意:** 如果你已经用Remix编译了智能合约，请直接跳过此部分。

本指南介绍了使用 [Waffle](https://github.com/EthWorks/Waffle)创建和部署基于Solidity的智能合约到Acala独立节点的过程。Waffle是Ethereum上智能合约常用的开发框架之一。

## **1. 确认准备工作**

首先，你需要安装Node.js (在本示例中，我们使用 v15.x版本) 和 npm 包管理器. 关于安装问题，请按照官方文档的指导，选择你的运行系统进行安装：[安装 NodeJS](https://nodejs.org/en/download/package-manager/)

我们可以通过查询每一个包的版本来确认是否已经安装完毕：

```
node -v
```

```
npm -v
```

安装yarn包管理器:

```
npm install --global yarn
```

检查是否已经安装正确:

```
yarn -v
```

## **2. 使用Waffle**

通过收集所需要的在[AcalaNetwork/evm-examples](https://github.com/AcalaNetwork/evm-examples) repo中的dependencies, 我们已经让Waffle的使用非常便捷。&#x20;

只需克隆repository 和安装 dependencies.

```
git clone https://github.com/AcalaNetwork/evm-examples
cd evm-examples/erc20

yarn install
```

## **3. 从零使用Waffle  (可选)**

或者，你可以按照如下方法一个个安装library：

创建一个项目文件夹 `smart-contract-waffle`

```
mkdir smart-contract-waffle
cd smart-contract-waffle
```

初始化包管理器

```
yarn init -y
```

安装所有如下的dependencies

```
yarn add --dev @openzeppelin/contracts@3.3.0 ethereum-waffle@3.2.1
```

注意：建议按照指定的准确版本安装依赖关系，以避免破坏性变化

然后创建一个waffle设置文件

```
touch waffle.json
```

将如下内容复制到 `waffle.json` 文件

```
 {
    "compilerType": "solcjs",
    "compilerVersion": "0.6.2",
    "sourceDirectory": "./contracts",
    "outputDirectory": "./build"
  }
```

这将设置 `0.6.2`版本的solidity编译器，从 `./contracts` 文件夹中编译合约，并将字节码输出和ABI文件保存到 `./build` 文件夹中

现在创建 `./contracts` 文件夹，并添加到 `BasicToken.sol` 合约中。

```
mkdir contracts
touch contracts/BasicToken.sol
```

将如下内容复制到 `BasicToken.sol` 文件中并保存。

```
pragma solidity ^0.6.0;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

// Example class - a mock class using delivering from ERC20
contract BasicToken is ERC20 {
    constructor(uint256 initialBalance) public ERC20("Basic", "BSC") {
        _mint(msg.sender, initialBalance);
    }
}
```

## **4. 编译智能合约**

现在编译合约到ABI 和字节码中. 在终端中运行如下代码：

```
yarn waffle
```

## **5. 获取ABI文件**

Waffle然后生成输出文件 `./build/BasicToken.json` 到 `./build` 文件夹。

请注意，该文件要与Remix创建的文件一样。

Waffle也提供了一整套测试工具，查阅他们的文档和代码示例[这里](https://github.com/EthWorks/Waffle)。
