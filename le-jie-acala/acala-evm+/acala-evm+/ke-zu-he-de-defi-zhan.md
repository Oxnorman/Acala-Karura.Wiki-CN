# 可组合的Defi栈

### 在EVM和Runtime中可完全组合的DeFi基础产品组件

部署在Acala EVM中的智能合约Dapps可以直接使用原生和跨链资产，如DOT、ACA、aUSD、renBTC等。部署在EVM中的ERC-20 Token也可以在Runtime层面部署，在DEX上所或者（通过“治理”批准）作为手续费Token使用。例如，Ampleforth将在Acala EVM上部署AMPL合约，这将使其成为原生Token，可以用来支付交易费用，并直接在我们的DEX上所。&#x20;

智能合约Dapps可以直接使用Acala DeFi基础产品组件（DeX、稳定币借贷和流动性质押）、桥、预言机等基础设施、原生和跨链的流动性可以组成各种有趣的DeFi应用，如借贷、特殊用途的DEX、基于质押的金融产品等。&#x20;

这个过程对用户和开发者来说是无感的，但在其背后的原生Token和协议（又称Runtime模块）是以预编译合约的形式在EVM中提供的。由EVM中的智能合约发起的交易被转换成Substrate交易，并可由任何Polkadot扩展程序使用polkadot.js签署。该响应将由SDK（[bodhi.js](https://github.com/AcalaNetwork/bodhi.js)）处理，并转换为Ethereum兼容的格式。&#x20;

### 可用的可组合合约&#x20;

这些预编译的合约现在已经提供给Acala EVM了&#x20;

* **ERC20中可用原生和跨链Token：**DOT, ACA, aUSD, XBTC, LDOT, RENBTC。在[这里](../../../jian-she-acala/jian-she-dapps/zhi-neng-he-yue/gao-ji/shi-yong-yuan-sheng-kua-lian-token.md)试试吧&#x20;
* 预言机合约获取喂价：这需要开放式预言机网关功能，如有保障的QoS。在[这里](../../../jian-she-acala/jian-she-dapps/zhi-neng-he-yue/gao-ji/shi-yong-yu-yan-ji-wei-jia.md)尝试。
* 链上自动调度器：实现订阅和定期付款等功能。在[这里](../../../jian-she-acala/jian-she-dapps/zhi-neng-he-yue/gao-ji/shi-yong-lian-shang-tiao-du-qi/)尝试。&#x20;
* 先进的合同部署功能，如状态租赁，以避免诈骗和链上资源的浪费。&#x20;
* 更多信息：我们正在逐步向Acala EVM添加更多原生功能，接下来是DeFi基本产品组件（DeX、稳定币借贷和流动性抵押）。&#x20;

点击[这里](https://github.com/AcalaNetwork/predeploy-contracts#predeployed-system-contract)了解更多关于这些合约的信息。
