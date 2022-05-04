# 如何改变默认手续费代币

## 默认手续费代币

您可以查看链上默认手续费代币的优先级排序，请跳转到 [Polkadot Webapp](https://polkadot.js.org/apps/) - 选择链（Acala或者Karura）

前往`Developer` - `Chain state` > `Constants` > `transactionPayment`

`defaultFeeSwapPathList`

![](<../../.gitbook/assets/image (7).png>)

在Acala网络上，手续费优先级是 ACA > aUSD > LCDOT > DOT.

如果用户的ACA余额不足以支付，系统将自动切换到aUSD作为手续费代币。

通过执行以下指令，用户可以自行设置下一个默认手续费代币：

&#x20;`1 transactionPayment.setAlternativeFeeSwapPath(fee_swap_path)`
