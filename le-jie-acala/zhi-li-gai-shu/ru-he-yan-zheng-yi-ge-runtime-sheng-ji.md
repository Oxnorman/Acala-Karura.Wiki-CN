# 如何验证一个Runtime升级

该指南使用runtime升级1.1.1版本作为示例。

一旦提出升级提案，你可以在这上面查阅到 [Polkadot App - Karura parachain - Democracy section](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkarura-rpc-2.aca-api.network%2Fws#/democracy).

![](https://1503523808-files.gitbook.io/\~/files/v0/b/gitbook-legacy-files/o/assets%2F-MAz4EenwXLth\_HO\_hmJ%2F-MeZWFC6SmWDZHsSjOYL%2F-MeZXYlfuyfZqQkjk66o%2FScreen%20Shot%202021-07-14%20at%2010.22.16%20PM.png?alt=media\&token=c6d5e41e-cf3f-4578-b685-21bf37227158)

## 升级Preimage信息 <a href="#upgrade-preimage-info" id="upgrade-preimage-info"></a>

扩展提案，找到Preimage信息。

* Preimage: `parachainSystem.authorizeUpgrade(0xd9660e7d73163f7b2e1591c08c60e68f4b47cb85dcba54d55c53b9573876f55e)`
* 哈希值: `0x4f8bf2c02c5a1e8cdcf7a94dabf2805c563c46a87876c684c5d79ffb745db115`

## 对代码进行验证 <a href="#verify-against-code" id="verify-against-code"></a>

在提案的讨论帖中，应提供发布标签，runtime WASM文件以及其他必要的信息，一边方便其他人对提交的preimage验证。

* 发布页面: [https://github.com/AcalaNetwork/Acala/releases/tag/1.1.3](https://github.com/AcalaNetwork/Acala/releases/tag/1.1.3)​
* Runtime Wasm: [https://gateway.pinata.cloud/ipfs/QmTrUJragkgGrp3eNyun7n7p5zT8MFLE3s87o3ZJSyj4wf](https://gateway.pinata.cloud/ipfs/QmTrUJragkgGrp3eNyun7n7p5zT8MFLE3s87o3ZJSyj4wf)​

### 采用如下步骤来验证 <a href="#take-the-following-step-to-verify" id="take-the-following-step-to-verify"></a>

#### 1. 为了发布，构建你自己的Wasm Runtime <a href="#1.-build-your-own-wasm-runtime-for-the-release" id="1.-build-your-own-wasm-runtime-for-the-release"></a>

* srtool 用于构建 wasm
  * 更多关于srtool的信息:
    * ​[https://www.chevdor.com/post/2019/12/06/srtool/](https://www.chevdor.com/post/2019/12/06/srtool/)​
    * ​[https://github.com/paritytech/srtool](https://github.com/paritytech/srtool)​
* 请按照如下步骤来构建
  * 安装 Docker
    * ​[https://docs.docker.com/get-docker/](https://docs.docker.com/get-docker/)​
  * 克隆Acala repo
    * `git clone https://github.com/AcalaNetwork/Acala.git`
  * 检查发布的branch
    * `git checkout release-karura-1.1.3`
  * 用 srtool 构建
    * `make srtool-build-wasm-karur`
  * 等待编译完成，你的wasm就好了

#### 2. 生成哈希值&并比较 <a href="#2.-generate-hash-and-compare" id="2.-generate-hash-and-compare"></a>

在 `Developer - Extrinsics` 中, 使用一下方法并上传wasm来生成调用哈希。将此哈希值与preimage的哈希值进行比对。

![](<../../.gitbook/assets/image (11).png>)
