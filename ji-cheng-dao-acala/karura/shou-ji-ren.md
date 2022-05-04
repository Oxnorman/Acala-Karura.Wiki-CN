# 收集人

## 概况 <a href="#overview" id="overview"></a>

收集人通过从用户收集平行链交易，和为中继链验证者产生状态转换证明来维护平行链。换句话说，收集人通过将平行链交易汇到平行链候选区块中，并根据这些区块为验证者产生状态转换证明来维护平行链。

虽然Karura的网络安全和共识（nPoS）由Kusama中继链的验证者集提供，但Karura的收集人将通过收集平行链交易供验证者验证来保持网络活跃。**与验证者不同，收集人与网络的安全性无关，作为一个平行链，网络默认是无需信任和去中心化的，一个平行链只需要一个诚实的收集人来抗审查即可。**在[这里](https://wiki.polkadot.network/docs/learn-collator)阅读更多关于收集人的信息。

Karura的收集人节点为Kusama中继链维护一个全节点服务，并为Karura网络提供一个全节点服务。每个服务都有自己的http/ws RPC端点、P2P端口等。Kusama全节点服务的基本路径位于Karura全节点服务的基本路径之内的。

## 收集人推广计划&#x20;

Karura采取分阶段的方式来推广收集人运作。由于收集人是非安全的关键性操作，一个平行链只需要一个诚实的收集人来抗审查，更多的收集人并不一定是好的，例如，它会降低网络的速度，收集人推出计划的设计首先目的是为了确保网络的稳定和运行。

#### **目前阶段：非公开收集人集合**

#### **第0阶段：非公开收集人集合**

Karura网络创世于2021年6月23日。创世后，Karura的网络安全和共识是由Kusama 中继链的nPoS验证人提供。就像Statemint（Kusama上的公益资产平行链）一样，Karura的收集人最初将由Acala基金会代为运行，直到收集人软件稳定并可以向更广泛的社区发布。

#### **第一阶段：授权收集人集合（我们现在位置）**

经治理批准，Karura将随后向授权的收集人开放收集人集合。虽然这些授权的收集人没有区块奖励，也没有额外的激励措施，但他们的节点服务会由Acala基金会支付合理的费用。

这些收集人都是有经验、有信誉的节点服务提供商，他们有良好的服务历史，并全身心致力于服务整个网络。预计在这个阶段仍然会有很多混乱或者软件升级，这些收集人需要与核心开发团队密切合作，以确保网络的稳定性。

预计Karura网络将保持这样一个授权的收集人集合，直到网络完全稳定、收集人质押模块和奖励计划完全实施和审计之后才会结束。

#### 第二阶段：公共收集人集合&#x20;

经治理批准，Acala随后将启用收集人无需权限的选举，并启用收集人奖励。考虑到收集人是非安全的关键因素这一事实，一个平行链只需要一小组收集人来确保有效性和抗审查性，奖励计划将相应地反映这一点。

你可以通过填写[这个表格](https://docs.google.com/forms/d/e/1FAIpQLSeEl9KI0baZQXlPXoXB-tP9axe7kyHSJlx4rNAJ0kqij4SW6A/viewform?usp=send\_form)申请成为Acala网络（以及后来的Acala网络）的收集人/有效性提供者。

你可以在我们的Discord上订阅[节点运营商-公告频道](https://discord.com/invite/uWSZWsUcEn)，以获得更新和突发变化。&#x20;

## 收集人节点 <a href="#collator-node" id="collator-node"></a>

### 配置要求 <a href="#spec-requirement" id="spec-requirement"></a>

与[ Kusama验证人节点要求](https://guide.kusama.network/docs/maintain-guides-how-to-validate-kusama/#requirements) 一致

### 运行节点 <a href="#run-node" id="run-node"></a>

参考[全节点指南](../acala-wang-luo/quan-jie-dian.md)

### 收集人配置 <a href="#collator-configuration" id="collator-configuration"></a>

#### **秘钥管理** <a href="#key-management" id="key-management"></a>

Karura 收集人需要Aura会话key.RPC  `author_rotateKeys`或 `author_insertKey` 来升级会话秘钥。

#### **注册** <a href="#registration" id="registration"></a>

* Karura 当前正在使用来自Statemint的 `collectorSelection` pallet 来处理收集人的注册问题。在授权验证人集合阶段，所需的候选人资格保证金将会是一个极其高价格，这样避免了一般公众进行登记。
* 授权的提供商需要递交Aura会话秘钥中的公钥给收集人

#### CLI <a href="#cli" id="cli"></a>

* `--collator` 为平行链部分

### **CLI 示例** <a href="#example-cli" id="example-cli"></a>

```
--base-path=/acala/data
--chain=karura
--name=collator-1
--collator
--execution=wasm
--
--chain=kusama
```
