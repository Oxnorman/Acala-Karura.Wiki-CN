# 指南

在本教程中，我们将利用Acala的链上调度器来创建一个自动订阅服务，根据用户订阅的时间来奖励他们。用户可以订阅这项服务，每隔一段时间，合同就会奖励他们一些token。&#x20;

## 设置&安装 Dependencies

我们将从零构建一个项目，用Waffle建设和测试。如果你想用Remix来构建你的合约，请参阅[文章](../../kai-shi/shi-yong-remix.md)。

首先，如果你没安装`nodejs` 和yarn，请运行如下：

```
sudo apt install -y nodejs

npm install --global yarn
```

下一步，在你希望你项目上线的文件夹内运行如下指令：

```
mkdir subscription-contract
cd subscription-contract

yarn init -y
yarn add --dev ethereum-waffle@3.2.1
```

添加如下script 到你的 `package.json`:

```
"build": "waffle"
```

这将为我们的项目创建一个文件夹，初始化一个新的yarn项目，并将waffle作为一个开发依赖。

我们将使用waffle来编译我们的智能合约。 在你的项目文件夹中，创建一个名为waffle.json的文件，并在该文件中粘贴以下内容。

```
{
  "compilerType": "solcjs",
  "compilerVersion": "0.6.2",
  "sourceDirectory": "./contracts",
  "outputDirectory": "./build"
}
```

在建设你的智能合约时，本文为配置 `waffle` 以便使用

让我们一起来创建 `contracts` 文件夹

```
mkdir contracts
```

## 使用 Scheduler.sol

`contracts` 文件夹内，创建 `Scheduler.sol` 然后粘贴如下指令：

```
pragma solidity ^0.6.0;

abstract contract Scheduler {
    // Schedule a contract call.
    function scheduleCall(
        address contract_address, // The contract address to be called in future.
        uint256 value, // How much native token to send alone with the call.
        uint256 gas_limit, // The gas limit for the call. Corresponding fee will be reserved upfront and refunded after call.
        uint256 storage_limit, // The storage limit for the call. Corresponding fee will be reserved upfront and refunded after call.
        uint256 min_delay, // Minimum number of blocks before the scheduled call will be called.
        bytes memory input_data // The input data to the call.
    )
    virtual
    public
    returns (uint256, uint256); // Returns a task id that can be used to cancel or reschedule call.
}
```

这个文件描述了调度器智能合约以及你必须向它提供哪些参数才能使用它。但是调度器是如何工作的呢？&#x20;

Acala EVM为Solidity、Substrate和Web3开发者提供了完整的全栈（Acala+EVM+Substrate+WASM）体验，可与一个钱包无缝衔接。许多Substrate和WASM的定制在EVM内部通过预编译的合同提供，如链上调度器、自带手续费、QoS预言机喂价等等。它允许我们添加在以太坊上不可能实现的新功能，同时仍然让开发者使用现有的代码和工具来创建基于这些功能的DApps。这些预编译的智能合约在Acala EVM上有静态且已知的地址，使得它非常容易使用。

## 创建订阅合约

通过在`contracts`文件夹中建立`Subscription.sol`来创建智能合约文件。在智能合约文件中添加如下代码：

```
pragma solidity ^0.6.0;

import "./Scheduler.sol";

contract SubscriptionToken {
    Scheduler scheduler;
    constructor(address scheduler_address) public payable {
        scheduler = Scheduler(scheduler_address);
    }
}
```

这里你可以看到我们正在导入一个抽象类，主要描述Scheduler智能合约，并在构造函数中把我们的调度器指向它的地址。同样，调度器是一个预编译的智能合约，有一个静态地址。该地址将永远保持活跃，也不需要部署你自己的版本。

![](https://i.imgur.com/8d8Mxly.png)

### 构造函数

接下来，让我们设置一些状态变量并修改一个构造函数，在合约中添加如下代码：

```
contract SubscriptionToken {
    uint period;
    address[] subscribers;
    mapping(address => uint) public balanceOf;
    Scheduler scheduler;

    constructor(uint _period, address scheduler_address) public payable {
        period = _period;
        scheduler = Scheduler(scheduler_address);
        scheduler.scheduleCall(address(this), 0, 50000, 100, period, abi.encodeWithSignature("paySubscribers()"));
    }
}
```

这里我们添加6个状态变量。让我们一个个看看他们的内容：

1. `balanceOf`: 定义/展示在用户余额中原生token的数量
2. `period`: 一段时间内，调度器应该调用的区块数量

构造函数是自我声明的，他所做的就是为合约设置第一个状态变量。

### 订阅和转账功能

下一步让我们添加 `订阅功能`

```
contract SubscriptionToken {
  ...

  function subscribe() public {
        subscribers.push(msg.sender);
  }
  function transfer(address _to, uint amount) public {
        require(balanceOf[msg.sender] > amount -1, "Insuffcient funds");
        balanceOf[msg.sender] -= amount;
        balanceOf[_to] += amount;
  }

}
```

这里的订阅功能仅仅只是添加用于到一个名单中，名单里的人将会收到分发的token。

最后，我们再看一下 `scheduleCall`的参数。

```
scheduler.scheduleCall(address(this), 0, 50000, 100, period, abi.encodeWithSignature("paySubscribers()"));
```

让我们分析一下上面这段代码:

* `address(this)` 是要调用的智能合约的地址，在这种情况下，我们调用的是智能合约与调用schedule合约的是同一个智能合约
* `value` - 调用时要单独发送多少原生token
* `gas_limit` - 调用时消耗的gas上限。相应的费用将被预先保留，并在调用后退还。&#x20;
* `storage_limit` - 调用的存储极限。相应的费用将被预先保留，并在调用后退还
* `min_delay` 是指从现在开始它应该尝试和执行这个调用的区块数量（尽管它可能很多！）
* `abi.encodeWithSignature("paySubscribers()")` 在智能合约内调用的功能（下面我们会对其进行定义）。

对于其他参数传递到 `scheduler` 合同的信息， 向上滚动到我们创建的`Scheduler.sol`.

### Pay subscribers

现在我们创建scheduler正被调用的 `paySubscribers` 功能：

```
contract SubscriptionToken {
  ...

  function paySubscribers() public {
        require(msg.sender == address(this));
        if (subscribers.length > 0) {
            for (uint256 i = 0; i < subscribers.length; i++) {
                address subscriber = subscribers[i];
                balanceOf[subscriber] += 1;
            }
        }

        scheduler.scheduleCall(address(this), 0, 50000, 100, period, abi.encodeWithSignature("paySubscribers()"));
    }
}
```

请注意该功能的第一行代码：

```
require(msg.sender == address(this), "No Permission");
```

上面这行代码表示只有合约本身可以调用这个函数。当我们使用`Scheduler`合约安排一个调用时，实际上并不是scheduler在调用这个函数，而是这个函数本身。Scheduler只是在以后的时间里调度这个调用。&#x20;

就这样了! 我们现在有了一个具有自动订阅功能的智能合约

## 建设

在项目根文件目录上运行如下代码，即可建造智能合约：

```
yarn build
```

## 部署

请按照如下指导部署智能合约[这里](../../kai-shi/bu-shu-he-yue.md).

你可以设置 `period` 为1 (也就是大约6 secs), 然后找到 scheduler 地址，也就是在预部署合约的列表中。

![](https://i.imgur.com/NX3iQUW.png)

当所有事情已经完成，点击部署。

## 执行合约

得到新token的唯一方式就是订阅该智能合约t。执行 `subscribe` 功能和检查随着订阅者的加入，余额是如何变化的。
