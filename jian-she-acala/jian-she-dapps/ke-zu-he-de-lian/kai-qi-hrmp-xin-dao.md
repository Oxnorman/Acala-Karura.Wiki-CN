# 开启HRMP信道

(原始的hackmd文件在[这里](https://hackmd.io/naPxPYPYSXOlK0L7WohVdQ?view))

开启HRMP信道步骤:

1. 发送方平行链发送一个初始化开启信道请求
2. 接收方平行链接受请求

如上步骤通过发送方或者接收方的`Xcm::Transact` 完成的。

在Karura和Statemine双向通道通信的例子中，有两个步骤需要在每个平行链端完成：

Karura:

* `hrmpInitOpenChannel(1000)` : 向Statemine发起打开HRMP信道的请求
* `hrmpAcceptOpenChannel(1000)` : 接受Statemine的HRMP通道请求

Statemine:

* `hrmpInitOpenChannel(2000)` : 向Karura发起开放HRMP通道请求。
* `hrmpAcceptOpenChannel(2000)` : 接受来自Karura的HRMP通道请求

如果Karura和Statemine只有一个单一方向的通道，只允许Karura到Statemine，而不允许Statemine到Karura，那么每一边只需要做一个步骤：

* Karura: `hrmpInitOpenChannel(1000)`: 向Statemine发起打开HRMP通道的请求
* Statemine: `hrmpAcceptOpenChannel(2000)` : 接受来自Karura的HRMP通道请求。

在下面的例子中，我们正在做Karura到Statemine的单方向开放通道。

## 发送初始开放通道请求

### 产生编码的交易

在PolkadotJS应用程序中，切换到实时Polkadot/Kusama网络。转到**开发者->Javascript**部分。运行编码代码，注意用你的收件人替换演示收件人平行链id `1000`。

```javascript
const tx = api.tx.hrmp.hrmpInitOpenChannel(1000, 1000, 102400);
console.log(tx.toHex());
```

结果会像 `0x3c043c00e8030000e803000000900100`, 去掉前面的十六进制`3c04`编码的结果是 `0x3c00e8030000e803000000900100`.

### 发送请求

前往PolkadotJS app, 转换到发送方平行链（这里是Karura）。前往**Developer -> Sudo** 部分.

使用 `ormlXcm -> sendAsSovereign` 来发送交易. XCM的消息格式(v2):

请注意这里有两个数据域需要被修改：

* \<relay-chain-encoded-hex-call>: `0x3c00e8030000e803000000900100`
* \<parachain-id>: 2000

> 请注意， parachain-id 就是你的平行链, Karura的平行链ID是2000

```
ormlXcm.sendAsSovereign(
  dest: XcmVersionedMultiLocation
  {
    V1: {
      parents: 1
      interior: Here
    }
  }
  
  message: XcmVersionedXcm
  {
    V2: [
      {
        WithdrawAsset: [
          {
            id: {
              Concrete: {
                parents: 0
                interior: Here
              }
            }
            fun: {
              Fungible: 1,000,000,000,000
            }
          }
        ]
      }
      {
        BuyExecution: {
          fees: {
            id: {
              Concrete: {
                parents: 0
                interior: Here
              }
            }
            fun: {
              Fungible: 40,000,000,000
            }
          }
          weightLimit: Unlimited
        }
      }
      {
        Transact: {
          originType: Native
          requireWeightAtMost: 1,000,000,000
          call: {
            encoded: <relay-chain-encoded-hex-call>
          }
        }
      }
      {
        DepositAsset: {
          assets: {
            Wild: All
          }
          maxAssets: 1
          beneficiary: {
            parents: 0
            interior: {
              X1: {
                Parachain: <parachain-id>
              }
            }
          }
        }
      }
    ]
  }
)
```

为了确认请求已经发送，请转到Polkadot/Kusama, 前往 **Developer -> Chain State**, 检查 **hrmp -> hrmpOpenChannelRequests**.

## 接受开放信道请求

### 产生编码交易

在PolkadotJS 应用中， 切换到实时的Polkadot/Kusama网络. 前往 **Developer -> Javascript** ，运行编码代码，注意用你的收件人提供演示收件人 para id `2000` ：

```javascript
const tx = api.tx.hrmp.hrmpAcceptOpenChannel(2000);
console.log(tx.toHex());
```

结果会像`0x1c043c01d0070000`, 去掉前面的16进制 `1c04`, 编码的结果是 `0x3c01d0070000`.

### 发送请求

前往PolkadotJS app, 转换到接收方平行链。前往**Developer -> Sudo** 部分.

使用 `ormlXcm -> sendAsSovereign` 来发送交易. XCM的消息格式(v2):

请注意这里有一个数据域需要被修改：

* \<relay-chain-encoded-hex-call>: `0x3c01d0070000`

```
ormlXcm.sendAsSovereign(
  dest: XcmVersionedMultiLocation
  {
    V1: {
      parents: 1
      interior: Here
    }
  }
  
  message: XcmVersionedXcm
  {
    V2: [
      {
        WithdrawAsset: [
          {
            id: {
              Concrete: {
                parents: 0
                interior: Here
              }
            }
            fun: {
              Fungible: 1,000,000,000,000
            }
          }
        ]
      }
      {
        BuyExecution: {
          fees: {
            id: {
              Concrete: {
                parents: 0
                interior: Here
              }
            }
            fun: {
              Fungible: 40,000,000,000
            }
          }
          weightLimit: Unlimited
        }
      }
      {
        Transact: {
          originType: Native
          requireWeightAtMost: 1,000,000,000
          call: {
            encoded: <relay-chain-encoded-hex-call>
          }
        }
      }
      {
        DepositAsset: {
          assets: {
            Wild: All
          }
          maxAssets: 1
          beneficiary: {
            parents: 0
            interior: {
              X1: {
                Parachain: <parachain-id>
              }
            }
          }
        }
      }
    ]
  }
)
```
