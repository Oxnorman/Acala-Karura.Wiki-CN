# 节点交互

本文将指导你如何与你的节点进行一些基本的互动。记得要多查看你常用工具的文档。本指南旨在指导你使用合适的工具，并不应当看做是标准参考。

* [Substrate RPC API](https://crates.parity.io/sc\_rpc\_api/index.html)
* [Polkadot JS RPC 文档](https://polkadot.js.org/docs/api/)
* [Substrate API Sidecar](https://github.com/paritytech/substrate-api-sidecar)

### RPC

基于Substrate链的客户端开放HTTP和WS 端点，以便进行RPC连接。HTTP的默认端口是 9933，WS的默认端口是9944。

为了获得所有RPC标准的清单，节点有一个叫做`rpc_methods` RPC端点。

比如：

```
$ curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "rpc_methods"}' http://localhost:9933/

{"jsonrpc":"2.0","result":{"methods":["account_nextIndex","author_hasKey","author_hasSessionKeys","author_insertKey","author_pendingExtrinsics","author_removeExtrinsic","author_rotateKeys","author_submitAndWatchExtrinsic","author_submitExtrinsic","author_unwatchExtrinsic","chain_getBlock","chain_getBlockHash","chain_getFinalisedHead","chain_getFinalizedHead","chain_getHead","chain_getHeader","chain_getRuntimeVersion","chain_subscribeAllHeads","chain_subscribeFinalisedHeads","chain_subscribeFinalizedHeads","chain_subscribeNewHead","chain_subscribeNewHeads","chain_subscribeRuntimeVersion","chain_unsubscribeAllHeads","chain_unsubscribeFinalisedHeads","chain_unsubscribeFinalizedHeads","chain_unsubscribeNewHead","chain_unsubscribeNewHeads","chain_unsubscribeRuntimeVersion","offchain_localStorageGet","offchain_localStorageSet","payment_queryInfo","state_call","state_callAt","state_getChildKeys","state_getChildStorage","state_getChildStorageHash","state_getChildStorageSize","state_getKeys","state_getKeysPaged","state_getKeysPagedAt","state_getMetadata","state_getPairs","state_getRuntimeVersion","state_getStorage","state_getStorageAt","state_getStorageHash","state_getStorageHashAt","state_getStorageSize","state_getStorageSizeAt","state_queryStorage","state_subscribeRuntimeVersion","state_subscribeStorage","state_unsubscribeRuntimeVersion","state_unsubscribeStorage","subscribe_newHead","system_accountNextIndex","system_addReservedPeer","system_chain","system_health","system_name","system_networkState","system_nodeRoles","system_peers","system_properties","system_removeReservedPeer","system_version","unsubscribe_newHead"],"version":1},"id":1}
```

给调用添加参数，比如通过哈希值获取区块:

```
$ curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "chain_getBlock", "params":["0x3fa6a530850324391fde50bdf0094bdc17ee17ec84aca389b4047ef54fea0037"]}' http://localhost:9933

{"jsonrpc":"2.0","result":{"block":{"extrinsics":["0x280402000b50055ee97001","0x1004140000"],"header":{"digest":{"logs":["0x06424142453402af000000937fbd0f00000000","0x054241424501011e38401b0aab22f4d72ebc95329c3798445786b92ca1ae69366aacb6e1584851f5fcdfcc0f518df121265c343059c62ab0a34e8e88fda8578810fbe508b6f583"]},"extrinsicsRoot":"0x0e354333c062892e774898e7ff5e23bf1cdd8314755fac15079e25c1a7765f06","number":"0x16c28c","parentHash":"0xe3bf2e8f0e901c292de24d07ebc412d67224ce52a3d1ffae76dc4bd78351e8ac","stateRoot":"0xd582f0dfeb6a7c73c47db735ae82d37fbeb5bada67ee8abcd43479df0f8fc8d8"}},"justification":null},"id":1}
```

一些返回值乍看之下可能没有意义。Substrate使用[SCALE 编码](https://substrate.dev/docs/en/knowledgebase/advanced/codec) 作为一种格式，它适用于资源受限的执行环境。你需要对信息进行解码，并使用[元数据](https://docs.substrate.io/v3/runtime/metadata/) (`state_getMetadata`) 来获取人类可读的信息。

#### 追踪链的头部

使用RPC端点 `chain_subscribeFinalizedHeads` 来订阅已上链区块头部的一系列哈希值，或者使用`chain_FinalizedHeads` 来获取已上链的最新区块头部的哈希值。使用 `chain_getBlock` 通过给定的哈希值获取区块位置。`chain_getBlock` 只接受区块哈希，所以如果你需要查询中间区块，请使用`chain_getBlockHash` 从区块高度来得到区块哈希值。

### Substrate API Sidecar

Parity团队维护着一个用TypeScript编写的RPC客户端， 他开放了一组有限的端点。他处理元数据和编解码逻辑，所以你只需要处理解码信息。他还汇聚了一个基础设施业务所需要的会计和审计的信息，比如交易费。

Sidecar可以提取区块，自动获得地址的余额（比如，有一个相应的区块高度数据就可以），获取链的元数据，获得一个预期交易费用并且将交易提交给节点的交易队列。如果你有任何功能/端点的要求，请在[repo](https://github.com/paritytech/substrate-api-sidecar)里标记这个问题 .

该客户端在HTTP主机上运行。下面的例子使用python3, 但是你可以在 `http://HOST:PORT/`以你喜欢的任何方式查询。默认地址是`http://127.0.0.1:8080`.

#### 获取一个区块

使用 `block/number` 端点来获取区块。为了得到链提示，请省略区块高度。

```
import requests
import json

url = 'http://127.0.0.1:8080/block/2077200'
response = requests.get(url)
if response.ok:
    block_info = json.loads(response.text)
    print(block_info)
```

这将返回一个完全解码的区块。在 `balances.transfer` extrinsic中，`partialFee` 项属于交易费的一部分。他被叫做“部分费用”，因为总费用包含小费字段。请注意，有些 extrinsics 是没有签名的，这些是内嵌的。

> 当跟踪交易费用时， `extrinsics.paysFee` 的值是不足以判断extrinsic是否包含费用的。该字段只表示如果递交一个交易，它就需要收费。为了收取一定费用，交易还需要被签名。所以在下面的例子里，`timestamp.set` extrinsic 不需要支付费用，因为它是内嵌的，有区块生产者放到区块里的

```
{'number': '2077200',
 'hash': '0x00e4e8bd8ec39e54aa26f01f5af7484d771f810fd7f1f4685a204dbc8fbfe80b',
 'parentHash': '0xf4065df1171047819592013770a98fff4b9058a96c4499676b72b1b93f5589e9',
 'stateRoot': '0xf1258925262058ef5d9eaaed49bd878e82584356f42aade40b68cdbd219be46c',
 'extrinsicsRoot': '0xbd4ea887b1a3cb3068db0524b938a0fb13093584b4e6664b3f121448a871cd3d',
 'logs': [{'type': 'PreRuntime',
   'index': '6',
   'value': ['BABE', '0x02b300000087b5c60f00000000']},
  {'type': 'Seal',
   'index': '5',
   'value': ['BABE',
    '0x689eddf91f1551f74de96ab0e2e52f41522bd82920cbe595148f873aa6d0541f48cfbb9b281181f2e52141b1c401dde7259634485fdab02cc7b63febe51ff78a']}],
 'onInitialize': {'events': []},
 'extrinsics': [{'method': 'timestamp.set',
   'signature': None,
   'nonce': '0',
   'args': ['1588085034000'],
   'tip': '0',
   'hash': '0x3cb46207ef8fadf3def3400ae2cb2a09b780431a6daf0b9bde15d91aeaf8faa3',
   'info': {},
   'events': [{'method': 'system.ExtrinsicSuccess',
     'data': [{'weight': '10000000', 'class': 'Mandatory', 'paysFee': True}]}],
   'success': True,
   'paysFee': True},
  {'method': 'finalityTracker.finalHint',
   'signature': None,
   'nonce': '0',
   'args': ['2077197'],
   'tip': '0',
   'hash': '0x2214831b2a13c75288d2267ebd089fffef82ba99d41f6c319ca06e24facc4d51',
   'info': {},
   'events': [{'method': 'system.ExtrinsicSuccess',
     'data': [{'weight': '10000000', 'class': 'Mandatory', 'paysFee': True}]}],
   'success': True,
   'paysFee': True},
  {'method': 'parachains.setHeads',
   'signature': None,
   'nonce': '0',
   'args': [[]],
   'tip': '0',
   'hash': '0xcf52705d1ade64fc0b05859ac28358c0770a217dd76b75e586ae848c56ae810d',
   'info': {},
   'events': [{'method': 'system.ExtrinsicSuccess',
     'data': [{'weight': '1000000000',
       'class': 'Mandatory',
       'paysFee': True}]}],
   'success': True,
   'paysFee': True},
  {'method': 'balances.transfer',
   'signature': {'signature': '0xf4cd36691d6ceb0a913e9d8409bde34e83761829f2fb25db15052de7ba9a6f7c4c54949f884d59005248c2c8b2951575ad0ae8f3c5d866e147a1771f47d91385',
    'signer': 'HUewJvzVuEeyaxH2vx9XiyAPKrpu1Zj5r5Pi9VrGiBVty7q'},
   'nonce': '155',
   'args': ['GoJ89MXptpNt1dH4NaZ73YtzknhrYeZcBJ33mifX5BMqoFz',
    '5000000000000'],
   'tip': '0',
   'hash': '0xc7b57537e2e63f866083ea22265cb65c846528d76378a3b3490eeada97f83d1d',
   'info': {'weight': '200000000', 'class': 'Normal', 'partialFee': '10000000000'},
   'events': [{'method': 'system.NewAccount',
     'data': ['GoJ89MXptpNt1dH4NaZ73YtzknhrYeZcBJ33mifX5BMqoFz']},
    {'method': 'balances.Endowed',
     'data': ['GoJ89MXptpNt1dH4NaZ73YtzknhrYeZcBJ33mifX5BMqoFz',
      '5000000000000']},
    {'method': 'balances.Transfer',
     'data': ['HUewJvzVuEeyaxH2vx9XiyAPKrpu1Zj5r5Pi9VrGiBVty7q',
      'GoJ89MXptpNt1dH4NaZ73YtzknhrYeZcBJ33mifX5BMqoFz',
      '5000000000000']},
    {'method': 'treasury.Deposit', 'data': ['8000000000']},
    {'method': 'balances.Deposit',
     'data': ['E58yuhUAwWzhn2V4thF3VciAJU75eePPipMhxWZe9JKVVfq',
      '2000000000']},
    {'method': 'system.ExtrinsicSuccess',
     'data': [{'weight': '200000000', 'class': 'Normal', 'paysFee': True}]}],
   'success': True,
   'paysFee': True}],
 'onFinalize': {'events': []}}
```

> The JS的number类型是53比特精确度的浮点数。 不能保证相应中的数字值会有一个数值类型。任何大于2\*\*53-1的数字都将有一个字符串类型。

#### 递交一个交易

使用Tx端点并以HTTP POST请求的方式，来递交一个序列化的交易，

```
import requests
import json

url = 'http://127.0.0.1:8080/tx/'
tx_headers = {'Content-type' : 'application/json', 'Accept' : 'text/plain'}
response = requests.post(
    url,
    data='{"tx": "0xed0...000"}', # A serialized tx.
    headers=tx_headers
)
tx_response = json.loads(response.text)
```

如果成功，端点将返回一个带有交易哈希的JSON。万一有错误发生，他会返回一个错误报告，比如：

```
{
    "error": "Failed to parse a tx" | "Failed to submit a tx",
    "cause": "Upstream error description"
}
```
