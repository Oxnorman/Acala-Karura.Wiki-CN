# 部署生态模块

下面是使用子模块在Runtime层面，用Acala进行构建项目的大致指南：

1. 项目组建立了子模块repo
2. 项目组在本地进行构建和测试
3. 项目组提交Repo供审查
4. Acala pulls在子模块中，通过runtime升级部署到测试网中
5. 安全审计
6. 治理

**1. 项目结构** 你将在你自己的repo中创建一个子模块，当它准备好时，我们可以把它拉到Acala的repo中。这使得你的代码库和许可证等具有独立性。

```
// on Acala side, folder structure as follows
- Acala repo
  - ecosystem-modules
    - your-sub-module
```

[示例 sub-module](https://github.com/AcalaNetwork/ecosystem-template/tree/f42c127bf10239821e1e7a56565cda4d64cd8d66). 你应该在你的组织中创建一个 repo，作为子模块使用。

你的子模块将被拉入Acala repo下的 [ecosystem-modules](https://github.com/AcalaNetwork/Acala/tree/master/ecosystem-modules) 。

**2. 本地测试** 分叉[Acala repo](https://github.com/AcalaNetwork/Acala), 将你的子模块拉入, 并在本地测试

**3. 提交代码供审查** Acala将在你的开发过程中提供技术支持，包括架构和技术指导，以及分享可用的库和标准。&#x20;

一旦你完成了开发，请提交你的 repo，我们的技术团队将帮助审查，并在拉入我们的 repo 之前提供反馈。

**4. 测试网部署** [Acala Mandala Test Network](https://wiki.acala.network/learn/get-started#mandala-test-network) 是一个实时的、无经济价值的测试网，用于验证新的链式逻辑和功能。你的模块一旦通过审查，就可以通过运行时升级部署到Mandala上。

**5. 审计** 模块级的集成在本质上改变了链条逻辑到Acala网络，虽然它为项目团队提供了最高水平的灵活性和定制能力，但它也使Acala有责任确保代码是安全的，并且不会对整个链条的运作造成意外的后果。因此，我们将对添加到Acala的模块进行安全审计，届时我们将与您联系。

**6. 治理** 在Karura 金丝雀网络（连接到Kusama）和主网（连接到Polkadot）上的部署将由各自的治理部门决定。
