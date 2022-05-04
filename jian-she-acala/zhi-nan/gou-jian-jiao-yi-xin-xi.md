# 构建交易信息

本文将讨论在Polkadot上的交易格式以及如何创建，签名和广播这些交易。不同于本指南其他章节，本章节会阐释一些可用的工具。**请记住，在集成时，一定要参考每个工具的说明文档。**

### 交易格式

Polkadot有一些基础的交易信息对所有的交易都是通用的。

* 地址: 经SS58加密的发送账户地址 address of the sending account.
* 区块哈希: 检查点区块的哈希值.
* 区块高度: 检查点区块的高度.
* 创世哈希: 链的创世哈希
* 元数据：在递交交易时，runtime的SCALE编码的元数据
* 随机数: 交易的随机数.\*
* 规格版本: runtime的当前规格版本
* 交易版本: 交易格式的当前版本
* 小费: 可选择的, 给小费可以提升交易的优先级
* 时代期: 可选择的， 交易在检查点后有效的区块数。如果为0，该交易会永远存在

\*从系统模块查询的随机数并不考虑待处理的事物，如果你想同时提交多个有效交易，你必须手动跟踪并增加随机数。

每个交易都会有自己（或者没有）参数添加。例如，余额Pallet中的 `transferKeepAlive` 功能会采用:

* `dest`: 目标地址
* `#[compact] value`:  token 数量 (压缩编码)

一旦你有了所有必需的信息，你就可以：

1. 构建一个未经签名的交易
2. 创建一个签过名的有效载荷.
3. 签署该有效载荷.
4. 将签名的有效载荷序列化为一个交易
5. 提交序列化的交易

Parity团队提供如下的工具来执行这些步骤。

### Acala JS

\[TODO]

### Tx Wrapper

如果你不想用CLI 进行签名操作，Parity提供了一个名为 [TxWrapper](https://github.com/paritytech/txwrapper) 的SDK可以以离线的方式生成和签署交易。 详见[案例](https://github.com/paritytech/txwrapper/tree/master/examples)。

**导入私钥**

```
import { importPrivateKey } from '@substrate/txwrapper';

const keypair = importPrivateKey(“pulp gaze fuel ... mercy inherit equal”);
```

**从公钥衍生出地址**

```
import { deriveAddress } from '@substrate/txwrapper';

// Public key, can be either hex string, or Uint8Array
const publicKey = “0x2ca17d26ca376087dc30ed52deb74bf0f64aca96fe78b05ec3e720a72adb1235”;
const address = deriveAddress(publicKey);
```

**构建离线交易**

```
import { methods } from "@substrate/txwrapper";

const unsigned = methods.balances.transferKeepAlive(
  {
    dest: "15vrtLsCQFG3qRYUcaEeeEih4JwepocNJHkpsrqojqnZPc2y",
    value: 500000000000,
  },
  {
    address: "121X5bEgTZcGQx5NZjwuTjqqKoiG8B2wEAvrUFjuw24ZGZf2",
    blockHash: "0x1fc7493f3c1e9ac758a183839906475f8363aafb1b1d3e910fe16fab4ae1b582",
    blockNumber: 4302222,
    genesisHash: "0xe3777fa922cafbff200cadeaea1a76bd7898ad5b89f7848999058b50e715f636",
    metadataRpc, // must import from client RPC call state_getMetadata
    nonce: 2,
    specVersion: 1019,
    tip: 0,
    eraPeriod: 64, // number of blocks from checkpoint that transaction is valid
    transactionVersion: 1,
  },
  {
    metadataRpc,
    registry, // Type registry
  }
);
```

**构建一个签名的有效荷载**

```
import { methods, createSigningPayload } from '@substrate/txwrapper';

// See "Construct a transaction offline" for "{...}"
const unsigned = methods.balances.transferKeepAlive({...}, {...}, {...});
const signingPayload = createSigningPayload(unsigned, { registry });
```

**序列化一个签过名的交易**

```
import { createSignedTx } from "@substrate/txwrapper";

// Example code, replace `signWithAlice` with actual remote signer.
// An example is given here:
// https://github.com/paritytech/txwrapper/blob/630c38d/examples/index.ts#L50-L68
const signature = await signWithAlice(signingPayload);
const signedTx = createSignedTx(unsigned, signature, { metadataRpc, registry });
```

**解码有效荷载类型**

在递交之前，你可能想解码有效荷载来验证内容

```
import { decode } from "@substrate/txwrapper";

// Decode an unsigned tx
const txInfo = decode(unsigned, { metadataRpc, registry });

// Decode a signing payload
const txInfo = decode(signingPayload, { metadataRpc, registry });

// Decode a signed tx
const txInfo = decode(signedTx, { metadataRpc, registry });
```

**检查交易哈希**

```
import { getTxHash } from ‘@substrate/txwrapper’;
const txHash = getTxHash(signedTx);
```

### 递交签名过的有效荷载

有多种方法来递交签过名的有效荷载：

1. 签署者的 CLI (`yarn run:signer submit --tx <signed-transaction> --ws <endpoint>`)
2. [Substrate API Sidecar](https://wiki.polkadot.network/docs/en/build-node-interaction#substrate-api-sidecar)
3. [RPC](https://wiki.polkadot.network/docs/en/build-node-interaction#polkadot-rpc) 带有 `author_submitExtrinsic` 或`author_submitAndWatchExtrinsic`, 后者为你订阅事件，以便在交易得到验证和被写入链中时，你可以得到通知。

### 注意事项

该示例当中使用的地址说明. 详细请见 [Subkey文档](https://substrate.dev/docs/en/knowledgebase/integrate/subkey).

```
$ subkey --network polkadot generate
Secret phrase `pulp gaze fuel ... mercy inherit equal` is account:
  Secret seed:      0x57450b3e09ba4598 ... ... ... ... ... ... ... .. 219756eeba80bb16
  Public key (hex): 0x2ca17d26ca376087dc30ed52deb74bf0f64aca96fe78b05ec3e720a72adb1235
  Account ID:       0x2ca17d26ca376087dc30ed52deb74bf0f64aca96fe78b05ec3e720a72adb1235
  SS58 Address:     121X5bEgTZcGQx5NZjwuTjqqKoiG8B2wEAvrUFjuw24ZGZf2

$ subkey --network polkadot generate
Secret phrase `exercise auction soft ... obey control easily` is account:
  Secret seed:      0x5f4bbb9fbb69261a ... ... ... ... ... ... ... .. 4691ed7d1130fbbd
  Public key (hex): 0xda04de6cd781c98acf0693dfb97c11011938ad22fcc476ed0089ac5aec3fe243
  Account ID:       0xda04de6cd781c98acf0693dfb97c11011938ad22fcc476ed0089ac5aec3fe243
  SS58 Address:     15vrtLsCQFG3qRYUcaEeeEih4JwepocNJHkpsrqojqnZPc2y
```
