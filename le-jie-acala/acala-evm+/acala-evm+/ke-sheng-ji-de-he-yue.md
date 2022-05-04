# 可升级的合约

## 可升级的智能合约

在Acala EVM中，开发者不再需要编写复杂的迁移合约来修复错误或对现有的应用程序进行改进。合约开发者可以简单地发送一个带有新合约字节码的交易来无缝升级合约，而不需要迁移用户或流动资金。&#x20;

为了减少直接在主网上测试所带来的风险，这里采用一个两阶段的部署过程来避免此问题

* **部署私有合同**：一旦合同被部署，它默认为对公众是私有的，只对`Contract Maintainer`（部署合同的人）和选择加入的开发者可见。所有必要的测试和最终验证都可以在公开之前完成。如果需要，`Contract Maintainer`也可以在这个阶段删除合同。&#x20;
* **部署公共合同**：`Contract Maintainer`可以将合同公开，即向公众开放业务。&#x20;

为了鼓励用户减少使用公共账本上的存储空间，同时也是为了有效地减少诈骗，我们使用`State Renting`（状态租赁）机制。`Contract Maintainer`在部署合同时需要交纳一笔保证金，当合同从链上删除时，保证金将被退还。&#x20;

多一些准入门槛会鼓励更多负责任的行为，当然我们也在不断研究这个问题，以实现更好的机制。