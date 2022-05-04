# 灵活的手续费

任何被接受的Token都可以作为Acala网络的交易费用。交易费用最终以网络原生TokenACA结算。因此，一个手续费Token必须有一个与Acala稳定币挂钩的流动性池，这将创建一个通往原生Token ACA的路径。&#x20;

如果默认Token的余额为零，系统将自动找到下一个可用和支持的手续费Token。

* Acala网络&#x20;
  * 默认的手续费Token：ACA&#x20;
  * 默认顺序: ACA > aUSD > DOT > LDOT&#x20;
* Karura网络&#x20;
  * 默认手续费Token：KAR&#x20;
  * 默认顺序: KAR > kUSD > KSM > LKSM
