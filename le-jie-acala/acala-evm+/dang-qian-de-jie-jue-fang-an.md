# 当前的解决方案

目前Substrate EVM兼容性解决方案，如[Frontier](https://github.com/paritytech/frontier)，是模拟以太坊节点的方式解决的。它的目的是实现全套以太坊的RPC以及模拟以太坊的出块过程。这样就允许当前以太坊的工具，比如Metamask以及Remix，与已启用Frontier的节点无缝衔接。

但集成Frontier暴露出了如下问题(按照严重程度排序）：

## 1. 被限制在EVM沙盒内

Frontier允许用户通过Metamask或其他现有的以太坊工具与EVM互动。但这些工具都还没有完全支持Substrate。Substrate原生模块的任何功能，比如Acala的DEX，支持多币种和跨链能力的token pallet，以及任何平行链建造的其他Pallet，比如Laminar的保证金交易Pallet，以上均不能通过Metamask或者其他以太坊工具进行访问。

这就意味着用户如果想感受Acala，Substrate或者Polkadot的强大功能，就需要同时使用Substrate钱包（比如Polkadot-js Extension）以及Metamask。

这对我们来说无疑是一个可以实现功能突破的地方。

## 2. 让节点更加昂贵

在设计Frontier时就希望使其承担更多任务。Substrate不会存储交易的哈希值或者历史事件，连事件过滤功能也没有。因而Substrate的节点在设计上就是轻量级的，来最大程度减少对资源的使用（比如磁盘空间\&CPU)。

另一方面，以太坊阶段允许用户用哈希值查询交易，并提供强大的事件日志查询API。Frontier则嵌有特殊的区块链导入逻辑，将交易和事件存储到链外的辅助存储中，以便支持以太坊查询所需的API。由于需要更强大的机器和更大的磁盘空间来操作一个节点，所以也就增加了维护成本。原本拥有一个轻量级节点可以降低任何地方的人运行节点的障碍，这有助于网络更加分散，但此方法却违背了该目标。

