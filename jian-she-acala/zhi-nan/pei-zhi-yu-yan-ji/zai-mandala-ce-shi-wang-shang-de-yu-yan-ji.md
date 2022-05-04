# 在Mandala测试网上的预言机

## 当前的预言机

* 你可以在[这里](https://github.com/AcalaNetwork/Acala/blob/master/primitives/src/lib.rs#L174) 找到当前可用的预言机服务提供商
* 在Mandala测试网上运行的Acala预言机， [在这里](https://acala-testnet.subscan.io/runtime/OperatorMembershipAcala?version=606)
* 提供链上喂价的Acala预言机运行人之一[这里](https://acala-testnet.subscan.io/account/5Fe3jZRbKes6aeuQ6HkcTvQeNhkkRPTXBwmNkuAPoimGEv45)

## 检查预言机状态

![](<../../../.gitbook/assets/1 (32).png>)

举例来说，检查Acala预言机状态，可以前往[Polkadot JS App](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fnode-6714447553211260928.rz.onfinality.io%2Fws#/chainstate) --> Developer --> Chainstate, 选择'acalaOracle' 以及其他查询参数，这样就可以查询运行人的会员状况以及token价格等。
