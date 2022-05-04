# 术语表

{% hint style="info" %}
需要添加Acala网络机制相关的词汇
{% endhint %}

### Acala <a href="#acala" id="acala"></a>

服务于稳定币和质押流动性的去中心化金融网络，以平行链的身份加入到的Polkadot网络中。

### ACA <a href="#aca" id="aca"></a>

Acala网络token的简写

### Attestation 证明 <a href="#attestation" id="attestation"></a>

在Polkadot有效性系统中，_attestation_ 是一种信息格式，验证人使用该信息来广播他们认为平行链候选区块是有效的还是无效的。

### Authority <a href="#authority" id="authority"></a>

Authority 是能够参与共识机制的区块链中角色的通用术语。在 GRANDPA 中，authority 要对他们认为是最终确认的链进行投票。在 BABE 中，authority 是出块者。Authority sets 可以通过像 Polkadot 的 NPoS 算法之类的机制来选出。

### BABE <a href="#babe" id="babe"></a>

\_B\_lind \_A\_ssignment of \_B\_lock \_E\_xtension 是Polkadot区块生产机制。

### Block 区块 <a href="#block" id="block"></a>

区块：一组数据集，比如交易数据，共同表明了区块链的状态转换。

### Block explorer 区块浏览器 <a href="#block-explorer" id="block-explorer"></a>

区块链浏览器：一个允许用户查看链上不同区块信息的应用。

### BLS <a href="#bls" id="bls"></a>

Boneh-Lynn-Shacham（BLS）签名的签名速度慢，验证速度则极其慢，需要缓慢且安全性低得多的配对友好曲线，并且往往具有危险的延展性。但是，BLS 允许多种多样的签名聚合选项阵列，远远超过任何其他已知的签名方案，这使 BLS 成为共识算法中投票和阈值签名的首选方案。

### Bonding 绑定 <a href="#bonding" id="bonding"></a>

绑定：代币被 "冻结 "以换取一些其他利益的过程。例如，质押就是绑定的一种形式，你通过为网络提供安全性来获得奖励。你也可以通过绑定代币来换取一个平行链插槽。

### Bridge 转接桥 <a href="#bridge" id="bridge"></a>

充当 Polkadot 中继链和外部链之间的中介的平行链，让中继链觉得该外部链是一条平行链（即满足 Polkadot 宿主对平行链的要求）。转接桥能让中继链与其他本身不兼容波卡的区块链之间进行交互，例如以太坊和比特币。

### Byzantine Fault Tolerance 拜占庭容错 <a href="#byzantine-fault-tolerance" id="byzantine-fault-tolerance"></a>

可以承受拜占庭式故障的系统的属性。也就是说，一个系统不仅单个子系统可能会发生故障，而且可能连特定子系统是否发生故障也不清楚。也就是说，系统上的不同观察者可能不会就系统是否发生故障达成共识。确保拜占庭容错能力是开发任何分布式系统的重要组成部分。

### Collator 收集人 <a href="#collator" id="collator"></a>

通过收集平行链交易并为验证人生成状态转换证明来维护平行链的节点。

### Consensus 共识 <a href="#consensus" id="consensus"></a>

一组实体就特定数据值达成一致的过程（例如对区块链上区块的排序和组成）。有多种用于确定共识的算法。Polkadot 使用的共识算法是 GRANDPA。

### Dapps 去中心化应用 <a href="#dapps" id="dapps"></a>

去中心化应用程序的通用术语，即作为分布式网络的一部分而不是在特定系统或一组系统上运行的应用程序。

### DOTs <a href="#dots" id="dots"></a>

Polkadot 的本地代币。DOT 具有以下三个目的：网络治理（允许 DOT 对网络升级和其他特殊事件进行投票）、常规运行（奖励好行为者和惩罚坏行为者）以及绑定（通过在连接中继器时“冻结” DOT 来添加新的平行链）。

### Duty Roster 值勤表 <a href="#duty-roster" id="duty-roster"></a>

一种查找表，该表指定了特定验证人需要执行的工作（即证明特定平行链的有效性）。值勤表通常将验证人集合按每个平行链随机分成不同的子集。

### Epoch <a href="#epoch" id="epoch"></a>

一个 Epoch 是 BABE 协议中的持续时间，分为几个较小的时隙。每个时隙都有至少一个有权提出封禁的时隙负责人。在 Kusama 中，它的持续时间与一个 session 相同。

### Era <a href="#era" id="era"></a>

等于一定数量的 Session（整数个），即重新计算验证人集（以及每个验证人的活跃提名人集）并支付奖励的时间段。

### Equivocation 重复签名 <a href="#equivocation" id="equivocation"></a>

向网络提供冲突的信息。BABE 的重复签名包括在同一插槽中创建多个区块。GRANDPA 的重复签名包括签署多个冲突链。

### Extrinsic <a href="#extrinsic" id="extrinsic"></a>

来自外部世界的状态更改，即它们不是系统本身的一部分。Extrinsics可以采取两种形式，即，"[inherents](https://wiki.polkadot.network/docs/en/glossary#inherent)" 和 "[transactions](https://wiki.polkadot.network/docs/en/glossary#transaction)"

### Finality 终结 <a href="#finality" id="finality"></a>

区块的不可逆性。通常，创建的区块要到将来某个时候才能终结，而在 “概率最终性” 的情况下可能永远不会终结。Polkadot 中继链使用称为 [GRANDPA](https://wiki.polkadot.network/docs/glossary) 的确定性终结工具。

### Finality Gadget 终结工具 <a href="#finality-gadget" id="finality-gadget"></a>

确定终结性的机制。

### Fisherman 钓鱼人 <a href="#fisherman" id="fisherman"></a>

监视网络的节点，以揪出行为不当的验证人或收集人。钓鱼人必须投入少量的 DOT，但是如果发现不良行为，则可以得到巨大的回报。

### Frame 框架 <a href="#frame" id="frame"></a>

由Substrate提供的pallet集合（substrate的runtime模块）

### Genesis 创世区块/创世期 <a href="#genesis" id="genesis"></a>

创世：一条区块链的初始，也就是区块0. 它也可以用来表示区块链的最初始状态，

> 例子： "在创世状态，Alice, Bob, 和Charlie每人有30个代币."

### Governance 治理 <a href="#governance" id="governance"></a>

确定哪些对网络的更改应该通过的过程，例如对代码的更改或资金的流动。Polkadot 的治理系统是链上的，并且基于利益相关者的投票。

### Governance Council 治理理事会 <a href="#governance-council" id="governance-council"></a>

一个由多个链上帐户组成的链上实体（最初是 6 个席位，最终增加到 24 个席位)。理事会可以充当 “被动”（未投票）利益相关者的代表。理事会成员有两项主要任务：为全体利益相关者团体投票进行全民公投，并取消恶意的全民公投。

### GRANDPA Finality Gadget GRANPA终结工具 <a href="#grandpa-finality-gadget" id="grandpa-finality-gadget"></a>

即 GHOST-based Recursive ANcestor Deriving Prefix Agreement。这是 Polkadot 的终结工具，它允许对区块链进行异步、负责和安全的终结。有关 GRANDPA 的概述，请参见以下 Medium 文章：[https://medium.com/polkadot-network/polkadot-proof-of-concept-3-a-better-consensus-algorithm-e81c380a2372](https://medium.com/polkadot-network/polkadot-proof-of-concept-3-a-better-consensus-algorithm-e81c380a2372)​

### Hard Fork 硬分叉 <a href="#hard-fork" id="hard-fork"></a>

区块链的永久性分流，可以通过共识规则中的高优先级更改快速发生。遵循硬分叉的客户端始终需要升级其客户端，才能继续遵循已升级的链。硬分叉被认为是链的永久性分歧，未升级的客户端所遵循的共识规则与升级的客户端所遵循的共识规则不兼容。

### Hard Spoon 硬汤匙 <a href="#hard-spoon" id="hard-spoon"></a>

Cosmos 的 Jae Kwon 将其定义为 “一条新链，它考虑了现有链的状态；其目的不是为了竞争，而是为了提供广泛的机会”。它是一条无争议的区块链，继承基础区块链的状态并创建同一区块链的新分支。

### Inherent <a href="#inherent" id="inherent"></a>

“本来就是真实的” Extrinsic。Inherents不会被 gossip 到网络上，而是由出块者放入区块中。由于它们并不像资金转账那样可证实，因此它们没有签名。区块链的runtime必须具有验证Inherents的规则。例如，时间戳是Inherents，通过落在每个验证人认为合理的范围内来进行验证。

### **Karura Network** <a href="#karura-network" id="karura-network"></a>

Karura是Kusama网络上的一个平行链，并且作为Acala的实验性网络。作为一个具有实际经济价值的实验性网络，Karura是一个协议升级的试验场，也是一个测试新DeFi协议和新链上治理方法的地方。

### KAR <a href="#kar" id="kar"></a>

Karura 网络代币的简称

### KSM <a href="#ksm" id="ksm"></a>

Kusama网络代币的简称.

### Kusama <a href="#kusama" id="kusama"></a>

是Polkadot的实验性网络。它由Polkadot软件的早期版本组成。它不是一个测试网 - 在过渡到NPoS之后，网络完全由社区（即Kusama代币持有人）掌握。

### LIBP2P <a href="#libp2p" id="libp2p"></a>

一个开放源代码库，用于进行加密的对等通信和其他网络功能。更多相关信息请访问: [https://libp2p.io/](https://libp2p.io)​

### Liveness 活跃性 <a href="#liveness" id="liveness"></a>

一种分布式系统的属性，即其最终将达到某种共识。陷入无限循环的系统被认为是非活跃的，即使计算仍在进行。最终提供结果的系统，即使结果不正确或花费很长时间才得出，也被认为具有活跃性。

### **Mandala Test Network** <a href="#mandala-test-network" id="mandala-test-network"></a>

一个无风险、无价值的游乐场，供我们、用户和开发者测试Acala的功能。

### Message 消息 <a href="#message" id="message"></a>

在 Polkadot 的 XCMP 协议中，消息可以是任意数据，该数据通过一个通道从一条平行链（出口链）发送到另一条（入口链），并由验证人集确保其传递。

### Message Queue 消息队列 <a href="#message-queue" id="message-queue"></a>

在 Polkadot 的 XCMP 协议中，消息队列是等待特定接收方平行链通过通道进行处理的消息列表。

### Node Explorer 节点浏览器 <a href="#node-explorer" id="node-explorer"></a>

一种为你提供有关节点的信息的工具，例如最新的区块、终结的区块以及该节点已知的当前链状态。

### Nominated Proof of Stake (NPoS) 提名权益证明（NPoS） <a href="#nominated-proof-of-stake-npos" id="nominated-proof-of-stake-npos"></a>

一种权益证明系统，提名人以自己的 stake 支持验证人，以表明对验证人良好行为有信心。提名权益股权证明与另一种更普及的概念 “委托权益证明Delegated Proof-of-Stake” 不同，提名人提名不合格的验证人将失去股份，而委托人却不会因验证人的行为而失去本金。请注意，其他一些区块链技术可能在委托人会被 slash 的情况下也依旧使用术语 Delegated Proof-of-Stake。Polkadot 使用 Phragmén 算法来将 stake 分配给被提名人。

### Nominator 提名人 <a href="#nominator" id="nominator"></a>

通过绑定其令牌来选择一组验证人进行提名的帐户。提名人会收到某些验证人的奖励，但是如果提名人的验证人行为不当，提名人也会受到 slash 惩罚。

### On-chain Governance 链上治理 <a href="#on-chain-governance" id="on-chain-governance"></a>

由区块链上的机制控制的区块链治理系统。链上治理允许以透明的方式做出决策。请注意，有多种不同的算法可以做出这些决策，例如简单多数投票、自适应投票偏差或基于身份的平方投票。

### Oracle 预言机 <a href="#oracle" id="oracle"></a>

预言机为Acala网络上的资产提供价格信息。

### Pallet <a href="#pallet" id="pallet"></a>

一个Substrate runtime模块

### Parachain 平行链 <a href="#parachain" id="parachain"></a>

满足多种特征的区块链，这些特征使其可以在 Polkadot Host 的范围内工作。也称为 “平行链”。

### Parachain Registry 平行链注册表 <a href="#parachain-registry" id="parachain-registry"></a>

一个相对简单的类似数据库的构造，在每个链上都包含静态和动态信息。

### Parity Technologies Parity科技 <a href="#parity-technologies" id="parity-technologies"></a>

由 Gavin Wood 博士和 Jutta Steiner 博士创立的公司，正在开发 Substrate 和 Polkadot。它还发布了其他几个项目，包括 Parity Ethereum 和 Parity Secret Store。

### Polkadot 波卡 <a href="#polkadot" id="polkadot"></a>

一个异构的多链网络，允许具有不同特征的各种区块链在共享安全性下执行任意的跨链通信。

### Proof of Stake (PoS) 权益证明 <a href="#proof-of-stake-pos" id="proof-of-stake-pos"></a>

一种选择共识系统参与者的方法，其中，根据参与者质押的代币数量（行为不当时代币有损失的风险）来选择参与者。通常，权益证明系统会限制参与者的数量。

### Proof of Validity 有效性证明 <a href="#proof-of-validity" id="proof-of-validity"></a>

平行链收集人提供的证明。基于此证明和平行链注册表，验证人可以验证平行链是否已正确执行其状态转换功能。有效性证明进入中继链区块。

### Proof of Work (PoW) 工作量证明 <a href="#proof-of-work-pow" id="proof-of-work-pow"></a>

一种选择共识系统参与者的方法，通常是最长链规则，参与者在其中尝试解决难题，例如找到哈希的部分原像。通常，工作量证明系统可以有任意数量的参与者。

### Proposal 提案 <a href="#proposal" id="proposal"></a>

潜在函数调用，需要在全民公投中进行投票。提案用于修改 Polkadot 网络的行为，这些行为包括细微的参数调整到替换 Runtime 代码。

### Random Seed 随即种子 <a href="#random-seed" id="random-seed"></a>

随机种子是链上可用的伪随机数。它被用在 Polkadot 协议的各个地方，在 [BABE ](https://wiki.polkadot.network/docs/glossary)出块机制中最为突出。

### Referendum 公投 <a href="#referendum" id="referendum"></a>

对于网络是否应接受某项提案进行的投票。公投可以由理事会、公众人士发起，也可以由先前提案的结果发起。利益相关者对公投进行投票，并由其 stake 规模（即质押的 DOT 数量）和他们愿意锁定其代币的时间权重进行加权。

### Relay chain 中继链 <a href="#relay-chain" id="relay-chain"></a>

协调平行链（和外部链，通过转接桥的方式）之间的共识和通信的链。

### Runtime <a href="#runtime" id="runtime"></a>

区块链的状态转换功能。它定义了一种有效算法，可以根据给定先前状态确定下一个区块的状态。

### Runtime Module <a href="#runtime-module" id="runtime-module"></a>

实现特定转换函数和功能的模块，人们可能需要在其 runtime 中用到某些模块。每个模块应具有特定领域的逻辑。例如，“余额” 模块具有处理帐户和余额的逻辑。在 Substrate 中，模块称为 “pallets”。

### Sealing 封装 <a href="#sealing" id="sealing"></a>

将区块添加到中继链的过程。请注意，区块终结是一个单独的过程 —— 区块在密封后的一段时间内终结。

### Session <a href="#session" id="session"></a>

Session 是 Substrate 实现中的术语，代表具有一组恒定的验证人的一段时间。验证人只能在 session 更改时加入或退出验证人集。

### Session Certificate <a href="#session-certificate" id="session-certificate"></a>

一条消息，其中包含所有 Session key 的串联签名。由 Controller 签名。

### Session Key  <a href="#session-key" id="session-key"></a>

验证人用于执行网络操作的热键，例如对 GRANDPA 提交消息进行签名。

### Shared Security 共享安全 <a href="#shared-security" id="shared-security"></a>

Polkadot 使用的安全模型，可以平等地保护所有链。它是通过将平行链区块的有效性证明放入中继链来实现的。有了共享安全模型，攻击者为了逆转单个平行链的最终确认状态，将需要攻击整个 Polkadot 系统。

### Slashing 罚币 <a href="#slashing" id="slashing"></a>

扣除一定比例的帐户 DOT，作为对验证人恶意或不当行为（例如重复签名或长时间离线）的惩罚。

### Soft Fork 软分叉 <a href="#soft-fork" id="soft-fork"></a>

客户端代码的向后兼容更改，使升级的客户端开始在新链挖矿。为了成功执行软分叉，需要大多数矿工的 “按哈希投票”。软分叉被视为区块链中的暂时分歧，因为未升级的客户端不遵循新的共识规则，但升级的客户端仍与旧的共识规则兼容。

### Staking 质押挖矿 <a href="#staking" id="staking"></a>

通过将代币作为 “抵押品” 来绑定代币（对于 Polkadot 来说即 DOT 代币）的行为，以产生有效的区块（从而获得区块奖励）。验证人和提名人将其 DOT 质押以保护网络。

### State transition function 状态转换函数 <a href="#state-transition-function" id="state-transition-function"></a>

描述如何改变区块链状态的函数。例如，它可以描述如何将代币从一个帐户转移到另一个帐户。

### Substrate <a href="#substrate" id="substrate"></a>

用于构建区块链的模块化框架。Polkadot 是使用 Substrate 构建的。使用 Substrate 构建的链很容易作为平行链连接。

### Transaction 交易 <a href="#transaction" id="transaction"></a>

已签名的外部信息。交易会散布在网络上，并产生交易费。交易是 “可证明的真实的”，与 inherent 不同。例如，一个人可以用自己的私钥在转移资金消息上签名，以此证明张三想向李四汇款。

### Validator 验证人 <a href="#validator" id="validator"></a>

一个节点，通过抵押 DOT 来确保中继链的安全，在平行链上验证来自收集人的证据，并与其他验证人一起对共识投票。

### Voting 投票 <a href="#voting" id="voting"></a>

利益相关者确定是否应通过某项公投过程。投票权由利益相关者帐户控制的 DOT 数量和他们愿意锁定其 DOT 的时间进行加权。

### Wallet 钱包 <a href="#wallet" id="wallet"></a>

一种程序，可以存储私钥并为 Polkadot 或其他区块链网络签署交易。

### Wasm <a href="#wasm" id="wasm"></a>

基于堆栈的虚拟机的指令格式。Polkadot Runtime Module 被编译为 Wasm。

### Watermark 水印 <a href="#watermark" id="watermark"></a>

在 Polkadot 的平行链消息传递方案中，水印是接收平行链的最小已处理发送高度。在水印时或之前发送到此平行链的所有通道上的所有消息都确保可以被处理。

### Web3 Foundation Web3基金会 <a href="#web3-foundation" id="web3-foundation"></a>

一个总部位于瑞士的基金会，致力于培养和管理去中心化网络软件协议领域的技术和应用，特别是那些利用现代密码学方法来保护去中心化网络，有利于 Web3 生态系统及其稳定性的技术和应用。

### WebAssembly <a href="#webassembly" id="webassembly"></a>

基于堆栈的虚拟机的指令格式。Polkadot Runtime Module 就被编译为 WebAssembly。也称为 Wasm。

### Witness 见证 <a href="#witness" id="witness"></a>

数据有效性的加密证明声明。
